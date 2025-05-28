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
Helps keep your project clean by avoiding duplicate hosts when importing multiple scan reports. Useful for merging partial scans or repeated results without clutter.

---

#### 📂 Files

| File                           | Description                                                   |
| ------------------------------ | ------------------------------------------------------------- |
| [`insert1.xml`](./insert1.xml) | First import — adds 3 new IPs to an empty project.            |
| [`insert2.xml`](./insert2.xml) | Contains 1 IP already imported in `insert1.xml` — skipped.    |
| [`insert3.xml`](./insert3.xml) | Contains 1 duplicate and 1 new IP — only the new IP is added. |

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
```
