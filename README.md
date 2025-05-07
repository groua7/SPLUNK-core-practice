# SPLUNK-core-practice
guide to install and practice Splunk for a cybersecurity analyst. you will need to create your account  and can use Kali Linux(if you want to) to do all




# 🟢 Splunk Core Certification Hands-On Lab

> Practice environment and exercises to prepare for the **Splunk Core Certified User** and **Power User** exams.

---

## 📌 What’s This About?

This repo provides a **self-paced, customizable practice lab** to learn and master Splunk fundamentals through real log data, search examples, dashboards, lookups, and more — all aligned with the Splunk certification objectives.

---

## 🖥️ 1. Prerequisites

- Splunk Enterprise (Free Trial): [Download Here](https://www.splunk.com/en_us/download/splunk-enterprise.html)
- Installed on: Windows / macOS / Linux
- Browser access: `http://localhost:8000`

---

## 📁 2. Project Structure

```bash
splunk-core-practice/
│
├── sample-data/              # Log files to index and analyze
│   └── web_access.log
│
├── saved-searches/           # Pre-written SPL queries
│   └── search-examples.txt
│
├── dashboards/               # XML dashboard files
│   └── sample-dashboard.xml
│
├── lookups/                  # Lookup CSV files
│   └── users.csv
│
└── README.md                 # This guide
````

---

## 📂 3. Load Sample Data

1. Go to **Splunk Web > Settings > Add Data**
2. Select **Upload** → upload `sample-data/web_access.log`
3. Set sourcetype to `apache_logs` (or create one)
4. Choose index (e.g., `practice_index`)
5. Click **Start Searching**

---

## 🔍 4. Run SPL Practice Searches

Open `saved-searches/search-examples.txt` and paste them in Splunk's Search bar.

```spl
# All data
index=practice_index

# Filter by status code
index=practice_index status=200

# Time-based search
index=practice_index earliest=-1h@h latest=now

# Field extraction via rex
index=practice_index | rex "GET\s(?<endpoint>/\S+)\sHTTP"

# Table format
index=practice_index | table _time, clientip, endpoint, status
```

---

## 📊 5. Create Dashboards

Use the UI or import `dashboards/sample-dashboard.xml`.

Example XML snippet:

```xml
<dashboard>
  <label>Web Traffic Overview</label>
  <row>
    <panel>
      <chart>
        <title>Requests per Hour</title>
        <search>
          <query>index=practice_index | timechart count by status</query>
        </search>
      </chart>
    </panel>
  </row>
</dashboard>
```

---

## 🔁 6. Lookups in Action

1. Upload `lookups/users.csv` in:
   **Settings > Lookups > Lookup table files**
2. Example CSV:

   ```csv
   ip_address,username
   192.168.1.5,john_doe
   10.0.0.1,jane_admin
   ```
3. Sample lookup search:

```spl
index=practice_index | lookup users.csv ip_address AS clientip OUTPUT username
```

---

## 🧪 7. Go Further (Custom Challenges)

* Extract new fields manually (Settings > Fields > Field Extractions)
* Create alerts (e.g., 5xx errors or login failures)
* Add firewall, syslog, or JSON logs
* Build your own dashboards and submit a Pull Request

---

## 📘 Resources

* [Splunk SPL Reference Guide](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Whatsinthismanual)
* [Splunk Core Certified User Exam Guide](https://www.splunk.com/en_us/training/certification/splunk-core-certified-user.html)
* [Practice Data Generator](https://github.com/splunk/eventgen)

---

## 🤝 Contribute

Have ideas or want to add your own use case or dataset? Fork this repo and submit a pull request!

---

## 🔐 License

MIT — free to use and adapt.

---

## 🙌 Author

Created for all aspiring Splunk professionals. You are not powerless — keep practicing, keep growing!

