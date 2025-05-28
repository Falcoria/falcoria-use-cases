📚 Part of the [Falcoria Documentation](https://falcoria.github.io/falcoria-docs/)

This page is part of the official use case library. It explains the behavior of the `replace` import mode — used when you want to **overwrite existing scan results with fresh data**.

Falcoria is a modular scan coordination system. To explore all available modes and understand where they apply (e.g., during scan configuration or manual imports), visit the [Import Modes](https://falcoria.github.io/falcoria-docs/scanledger/import-modes/).

### Import Mode: `replace`

Used for completely replacing scan data for any IPs already in the project. The `replace` mode ensures your project reflects the **most recent authoritative scan**.

---

#### 📌 Purpose

Clarify that:

* Existing IPs in the project will be fully replaced.
* All port data and service info for those IPs will be overwritten.
* New IPs not present in the project will be inserted.

---

#### 💡 Why It Matters

This mode is essential for long-term or frequently updated projects, where **scope changes rapidly** and **old scan results become misleading**. Typical scenarios:

- A system was reconfigured — ports opened/closed, services upgraded.
- You fixed an issue and want to verify the result.
- You're maintaining a live asset inventory and need to actualize findings.

`replace` mode ensures that outdated scan results are removed and replaced with the most recent scan output, reflecting the current state of the target systems.


---

#### 📂 Files

| File                             | IPs Included                              | Description                                                                 |
| -------------------------------- | ----------------------------------------- | --------------------------------------------------------------------------- |
| [`replace1.xml`](./replace1.xml) | 134.209.203.62, 159.223.15.22             | Initial scan — full port and service data for both IPs inserted.            |
| [`replace2.xml`](./replace2.xml) | 159.223.15.22, 188.166.121.245            | Replaces data for 159.223.15.22 and inserts a new IP (188.166.121.245).     |

---

#### 💻 Commands

Using [`falcli`](https://github.com/Falcoria/falcli):

```console
# Replace mode import
falcli project ips import --file replace1.xml --mode replace
```

Or using `curl`:

```console
curl 'http://<scanledger>/<project_uuid>/ips/import?mode=replace' \
  --header 'Authorization: Bearer <TOKEN>' \
  --form 'file=@"replace.xml"'
```

Repeat with `replace2.xml`.

---

#### ✅ Expected Result

After each step:

* `replace1.xml` → Project receives 2 full scan results.
* `replace2.xml` → One previously scanned IP is overwritten; one new IP is added.

Use this test to verify that your Falcoria instance correctly replaces old scan results with new ones, rather than merging or skipping them.

---

#### 🖥 Output Example

```console
python falcli.py project ips import --file replace1.xml --mode replace
Imported IPs report into project '4d8d98c5-522d-40ff-97a9-51052dfcf39a'. Result: 2 IPs.
```

Check data for IPs:
```console
python falcli.py project ips get
...
IP: 159.223.15.22
Status   : up
OS       : -
Hostnames: -

PORT   PROTO  STATE  SERVICE  BANNER                                                                                                
22     tcp    open   ssh      product: OpenSSH version: 8.9p1 Ubuntu 3ubuntu0.13 extrainfo: Ubuntu Linux; protocol 2.0 ostype: Linux
2121   tcp    open   ftp      product: Pure-FTPd                                                                                    
27017  tcp    open   mongod   -                                                                                                     
50443  tcp    open   unknown  -                                                                                                     
50777  tcp    open   echo     -                                                                                                     
53000  tcp    open   unknown  -  
```

Upload new report:
```console
python falcli.py project ips import --file replace2.xml --mode replace
Imported IPs report into project '4d8d98c5-522d-40ff-97a9-51052dfcf39a'. Result: 2 IPs.
```

Check for changes:
```console
python falcli.py project ips get
...
IP: 159.223.15.22
Status   : up
OS       : -
Hostnames: -

PORT  PROTO  STATE  SERVICE      BANNER
22    tcp    open   ssh          -     
2121  tcp    open   ccproxy-ftp  - 
```

Check statistics:
```console
python falcli.py project ips list
IP               PORT_COUNT
134.209.203.62   6         
159.223.15.22    2         
188.166.121.245  2       
```
