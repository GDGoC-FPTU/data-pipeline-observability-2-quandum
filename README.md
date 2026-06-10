[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112812&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** 2A202600786
**Name:** Trần Mạnh Chánh Quân

---

## Mo ta

Bai lab xay dung mot ETL Pipeline tu dong va khao sat anh huong cua chat luong du lieu len AI Agent (Data Observability).

Trong `solution.py` toi da hoan thanh 4 buoc:
- **Extract:** Doc du lieu tu `raw_data.json` (co xu ly FileNotFoundError va JSON loi).
- **Validate:** Loai bo cac record co `price <= 0` hoac `category` rong, dong thoi in so record giu lai va so record bi loai.
- **Transform:** Tinh `discounted_price = price * 0.9`, chuan hoa `category` ve Title Case va them cot timestamp `processed_at`.
- **Load:** Luu ket qua ra `processed_data.csv`.

Ngoai ra, toi chay `agent_simulation.py` voi du lieu sach va du lieu rac de so sanh va ghi nhan trong `experiment_report.md`.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# 1. Tao bo du lieu rac
python generate_garbage.py

# 2. So sanh phan hoi cua Agent voi du lieu sach vs du lieu rac
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- Pipeline doc 5 records tu `raw_data.json`, loai bo 2 records khong hop le (price <= 0 hoac category rong) va luu 3 records hop le ra `processed_data.csv`.
- Stress test: voi du lieu sach Agent tra loi dung ("Laptop at $1200"), con voi du lieu rac Agent bi danh lua boi outlier va tra loi sai ("Nuclear Reactor at $999999"). Chi tiet xem `experiment_report.md`.
