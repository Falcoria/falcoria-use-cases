📚 Part of the [Falcoria Documentation](https://falcoria.github.io/falcoria-docs/)

This page is part of the official use case library. It explains the behavior of the `insert` import mode — used when you want to **append new scan results** while keeping existing data untouched.

Falcoria is a modular scan coordination system. To explore all available modes and understand where they apply (e.g., during scan configuration or manual imports), visit the [Import Modes](https://falcoria.github.io/falcoria-docs/import-modes/).

### Import Mode: `insert`

Used for appending scan results without modifying existing data. The `insert` mode is ideal for non-destructive imports where duplicate IPs should be skipped silently.

---

#### 📌 Purpose

Clarify that:

* Existing IPs in the project are ignored.
* Only new IPs from the import file are added.

----

#### 💡 Why It Matters

This mode is useful when importing multiple scan reports that may contain overlapping data. It ensures that previously imported IPs are skipped, preventing duplicate entries. Typical use cases include:

- Merging partial scans performed at different times.
- Importing targeted service scans after an initial wide scan.
- Consolidating scan results from distributed scanning systems.

`insert` mode allows you to append new data to the project without altering or duplicating existing scan results.

---

#### 📂 Files

| File                             | IPs Included                                                | Description                                                                 |
| -------------------------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------- |
| [`insert1.xml`](./insert1.xml)   | 134.209.203.62, 159.223.15.22, 188.166.121.245              | First import — all IPs are inserted.                                        |
| [`insert2.xml`](./insert2.xml)   | 159.223.15.22                                               | Already seen — skipped entirely under `insert` mode.                        |
| [`insert3.xml`](./insert3.xml)   | 188.166.121.245, 128.199.62.51                              | 188.166.121.245 skipped; 128.199.62.51 is a new IP and gets inserted.       |


---

#### 💻 Commands

Using [`falcli`](https://github.com/Falcoria/falcli):

```console
falcli project ips import --file insert1.xml --mode insert
```

Or using `curl`:

```console
curl 'http://<scanledger>/<project_uuid>/ips/import?mode=insert' \
  --header 'Authorization: Bearer <TOKEN>' \
  --form 'file=@"insert1.xml"'
```

Repeat with other files.

---

#### ✅ Expected Result

After each step:

* `insert1.xml` → Project contains 3 IPs.
* `insert2.xml` → No change, 0 IPs added.
* `insert3.xml` → 1 new IP added; duplicate skipped.

Use this test to verify that your Falcoria instance correctly handles non-destructive inserts.

---

#### 🖥 Output Example

```console
python falcli.py project ips import --file insert1.xml --mode insert
Imported IPs report into project '4d8d98c5-522d-40ff-97a9-51052dfcf39a'. Result: 3 IPs.

python falcli.py project ips import --file insert2.xml --mode insert
No new IPs added in project '4d8d98c5-522d-40ff-97a9-51052dfcf39a'

python falcli.py project ips import --file insert3.xml --mode insert
Imported IPs report into project '4d8d98c5-522d-40ff-97a9-51052dfcf39a'. Result: 1 IP.

# Get statistics
python falcli.py project ips list
IP               PORT_COUNT
128.199.62.51    6         
134.209.203.62   6         
159.223.15.22    6         
188.166.121.245  8  
```
