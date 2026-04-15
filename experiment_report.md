# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600314
**Name:** Trần Tiến Dũng
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Dữ liệu đã được làm sạch, category đúng định dạng, không có outlier nên agent trả lời đúng. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Agent bị ảnh hưởng bởi outlier rất lớn nên đưa ra khuyến nghị sai với thực tế. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai với Garbage Data vì logic của script sẽ tìm sản phẩm electronics có giá cao nhất. Khi bộ dữ liệu chứa outlier như `Nuclear Reactor` giá `999999`, agent xem đó là lựa chọn tốt nhất dù nó vô lý trong thực tế. Ngoài ra, duplicate ID làm mất tính nhất quán của dữ liệu, wrong data type như `ten dollars` có thể gây lỗi hoặc làm lỗi quá trình xử lý, và null values ở `id` hoặc `category` làm giảm độ tin cậy của tập dữ liệu. Điều này cho thấy nếu không có ETL và validation trước, agent rất dễ học phải kiến thức rác và trả lời sai.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Tôi đồng ý. Prompt tốt không thể cứu được dữ liệu tệ vì trong thí nghiệm này, cùng một câu hỏi nhưng với dữ liệu đã làm sạch thì agent trả lời hợp lý, còn với garbage data thì agent đưa ra đáp án sai lệch.
