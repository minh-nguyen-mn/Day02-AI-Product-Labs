# 01 - Problem Scan & Filter Log
**Học viên:** Nguyễn Quang Minh

## 1. Problem Scan (5+ Problems qua 4 Lenses)

| STT | Lens | Bài toán cụ thể | Mô tả Pain Point & Hiện trạng |
|:---|:---|:---|:---|
| 1 | **Lặp lại** | Rebalancing danh mục định kỳ | Mỗi tuần phải chạy script Python, xuất CSV, so sánh với Target Weight và tạo file lệnh đặt mua (Order List) thủ công. |
| 2 | **Tốn thời gian** | Mapping mã chứng khoán (Ticker Mapping) | Dữ liệu từ Bloomberg (ticker), Reuters (RIC) và sở giao dịch (mã ISIN) không đồng nhất. Phải map bằng tay cho 2000+ mã. |
| 3 | **AI Fit** | Trích xuất dữ liệu từ BCTC (PDF) | Các báo cáo tài chính có cấu trúc khác nhau. Team phân tích phải đọc 100+ trang PDF để tìm chỉ số "Free Cash Flow" ẩn sâu trong thuyết minh. |
| 4 | **Pain từ người khác** | Giải trình danh mục (Attribution) | PM phàn nàn: "Số liệu nói mã A đóng góp 2% alpha, nhưng tôi không nhớ tháng qua mã A có tin tức gì đặc biệt để viết báo cáo cho khách hàng." |
| 5 | **AI có thể tốt hơn** | Backtest Strategy Logging | Hiện tại chỉ lưu kết quả Sharpe/Drawdown. AI có thể phân tích "tại sao chiến lược thua lỗ trong giai đoạn tháng 3" dựa trên dữ liệu vĩ mô. |

## 2. Quick Problem Cards (Top 3 chi tiết)

### Card #1: AI-Powered Financial Statement Extractor
- **Actor:** Junior Analyst (Team Research).
- **Workflow:** Tải PDF -> Ctrl+F tìm từ khóa -> Copy-paste vào Excel -> Kiểm tra chéo với ghi chú.
- **Bottleneck:** Bước trích xuất dữ liệu từ bảng biểu không định dạng (Unstructured tables). (⏱ 45 min/báo cáo).
- **Success Metric:** Trích xuất đúng 95% các chỉ số mục tiêu; Thời gian < 2 min/báo cáo.
- **Quick Gut:** **LLM Feature** (Cần khả năng hiểu ngữ cảnh bảng biểu phức tạp).

### Card #2: Automated Portfolio Attribution Commentary
- **Actor:** Portfolio Manager (PM).
- **Workflow:** Xuất file Attribution (%) -> Đọc tin tức lưu trữ -> Viết giải trình -> Gửi Compliance duyệt.
- **Bottleneck:** Kết nối giữa biến động số liệu và sự kiện thực tế (⏱ 180 min/tháng).
- **Success Metric:** Giảm thời gian từ 180 min -> 20 min; Nội dung bản thảo đạt 80% yêu cầu của Compliance ngay lần đầu.
- **Quick Gut:** **Agentic Workflow** (Cần truy cập Data số liệu + Tool tìm kiếm tin tức + Viết lách).

### Card #3: Intelligent Ticker Mapping Rule-Engine
- **Actor:** Data Ops.
- **Workflow:** Nhận file -> Tra cứu master data -> Mapping thủ công các mã lỗi.
- **Bottleneck:** Xử lý các mã chứng khoán mới hoặc bị đổi tên/hủy niêm yết (⏱ 30 min/ngày).
- **Success Metric:** Tự động mapping 99.9% mã; 0% lỗi sai sót trong báo cáo cuối ngày.
- **Quick Gut:** **No AI (Rule-based)** - Chỉ cần Fuzzy matching logic và Master Data tốt là đủ.

## 3. Kill Rationale & Selection
- **Kill Card #3:** Loại vì đây là bài toán Database/Rule-based điển hình. Dùng AI là lãng phí tài nguyên và không ổn định (Hallucination về mã chứng khoán là thảm họa).
- **Kill Card #1:** Tiềm năng nhưng độ phức tạp về OCR bảng biểu tài chính rất cao, cần hạ tầng kỹ thuật nặng.
- **Selected:** **Card #2 (Automated Portfolio Attribution Commentary)** vì có Impact lớn nhất đến PM và khả năng ứng dụng LLM/RAG là rất rõ ràng.