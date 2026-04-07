# 02 - Problem Deep-Dive: Automated Attribution Commentary

## 1. Problem Statement (6-Field)
- **Actor:** Portfolio Managers chịu trách nhiệm báo cáo quỹ định kỳ.
- **Current Workflow:** Lấy dữ liệu Brinson Attribution từ hệ thống (Data thô) -> Tra cứu tin tức doanh nghiệp tháng qua -> Viết 1-2 đoạn văn giải trình cho từng mã chiếm tỷ trọng lớn.
- **Bottleneck:** Việc tổng hợp thông tin định tính (Tin tức) để giải thích cho con số định lượng (Alpha %) cực kỳ rời rạc và tốn sức người.
- **Impact:** PM mất 2-3 ngày mỗi đầu tháng chỉ để viết báo cáo, dẫn đến phản ứng chậm với các cơ hội đầu tư mới.
- **Success Metric:** Thời gian hoàn thành bản thảo đầu tiên < 15 phút/danh mục (giảm 90%). PM chỉ cần sửa < 20% câu chữ.
- **Operational Boundary:** AI chỉ được sử dụng dữ liệu tin tức từ các nguồn tin cậy (Reuters, Bloomberg) cung cấp; AI KHÔNG được tự ý bịa ra lý do tăng/giảm nếu không tìm thấy dữ liệu nguồn; Phải có trích dẫn nguồn tin (Citation).

## 2. Success Metrics (Ngưỡng cụ thể)
- **Efficiency:** Processing Time giảm từ 180 phút xuống < 15 phút (Baseline: Danh mục 30 mã).
- **Quality (Consistency):** Điểm đánh giá mức độ chuyên nghiệp từ bộ phận Compliance đạt tối thiểu 4/5 (so với mức 3.5 hiện tại).

## 3. AI Fit Matrix & Alternatives
- **Alternatives:**
    - *Rule-based:* Không khả thi vì ngôn ngữ giải trình cần linh hoạt theo diễn biến thị trường.
    - *Template-based:* Quá khô khan, khách hàng sẽ nhận ra báo cáo máy móc.
- **AI Fit:** Chọn **LLM Feature (RAG - Retrieval Augmented Generation)**. 
    - *Complexity:* Cao (phải xử lý số liệu). 
    - *Ambiguity:* Trung bình (ngôn ngữ tài chính có chuẩn mực).

## 4. Sub-goals Decomposition
- **Trước khi dùng AI:** Hệ thống phải tự động chuẩn hóa file Excel Attribution thành định dạng JSON/Markdown mà LLM hiểu được.
- **Trong khi dùng AI:** User (PM) chọn mức độ "sâu" của báo cáo (Vắn tắt cho Retail hay Chi tiết cho Institutional).

## 5. Decision: GO (Pilot Phase)
**Lý thuyết hỗ trợ:** Dựa trên kết quả Research, các mô hình GPT-4o/Claude 3.5 Sonnet có khả năng phân tích dữ liệu bảng và viết lách tài chính xuất sắc. 
**Rủi ro:** Hallucination về số liệu. 
**Mitigation:** Thiết kế Prompt yêu cầu AI chỉ được sử dụng số liệu trong Input, tuyệt đối không tự tính toán lại.