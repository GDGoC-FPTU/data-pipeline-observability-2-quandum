# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600786
**Name:** Tran Manh Chanh Quan
**Date:** 2026-06-10

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Cau tra loi dung. Laptop la san pham electronics co gia hop ly nhat sau khi du lieu da duoc validate va transform. |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 2 | Cau tra loi sai/vo nghia. Agent bi danh lua boi outlier "Nuclear Reactor" gia 999999 va cac record loi khac. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi dung Garbage Data, Agent tra loi sai vi du lieu dau vao chua nhieu loi chat luong nghiem trong ma khong he duoc kiem tra truoc khi nap vao he thong. Thu nhat, bo du lieu co Extreme Outlier: san pham "Nuclear Reactor" voi gia 999999 da lam lech hoan toan logic idxmax() cua Agent, khien no chon mot ket qua vo ly thay vi Laptop. Thu hai, co Duplicate IDs (hai record cung id = 1) lam pha vo tinh duy nhat cua khoa, gay nhap nhang khi truy van. Thu ba, cot price ton tai Wrong Data Type ("ten dollars" la chuoi thay vi so), neu Agent thuc hien phep tinh so hoc thi se gay loi hoac ket qua khong xac dinh. Cuoi cung, cac Null values o id va category (record "Ghost Item") lam hong qua trinh loc theo category va co the gay crash. Tat ca cho thay rang neu khong co buoc validate va transform thi garbage in garbage out, Agent du thong minh den dau cung khong the dua ra cau tra loi dung tu nguon du lieu bi nhiem ban.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Du lieu chat luong quan trong hon prompt chat luong. Mot prompt duoc viet rat ky luong van se cho ket qua sai neu nguon du lieu chua outlier, sai kieu, trung lap hoac thieu gia tri, nhu thi nghiem da chung minh khi Agent chon "Nuclear Reactor". Nguoc lai, khi du lieu da duoc lam sach qua pipeline ETL (validate + transform), ngay ca mot logic Agent don gian cung dua ra cau tra loi chinh xac. Vi vay, dau tu vao Data Observability va kiem soat chat luong du lieu o tang pipeline la nen tang khong the thieu de xay dung mot he thong AI dang tin cay.
