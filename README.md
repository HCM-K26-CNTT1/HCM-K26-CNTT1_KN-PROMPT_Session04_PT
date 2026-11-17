# **BÀI TẬP: SO SÁNH TRADE-OFF CÁC GIẢI PHÁP RA LỆNH CHO KỸ THUẬT PROMPTING NÂNG CAO (LOGIC & CHUỖI)**

## **1. Đề xuất 2 giải pháp Prompt**

**Bối cảnh:** Cửa hàng online cần sử dụng AI để tự động kiểm tra đơn hàng, tính tổng tiền và phát hiện thông tin bị thiếu hoặc sai lệch.

**Giải pháp 1 – Prompt đơn giản:**

```
Bạn là trợ lý quản lý đơn hàng.
Hãy kiểm tra thông tin khách hàng, sản phẩm,
tính tổng tiền và phân loại đơn hàng.
Nếu thiếu dữ liệu, hãy thông báo lỗi.
Trình bày kết quả ngắn gọn, dễ hiểu.
```

**Giải pháp 2 – Prompt chi tiết:**

```
Bạn là chuyên viên xử lý đơn hàng online.

Hãy thực hiện theo quy trình Prompt Chaining gồm 3 bước:

Bước 1: Kiểm tra họ tên, số điện thoại, địa chỉ,
tên sản phẩm, số lượng và đơn giá.

Bước 2: Chỉ tính tổng tiền khi số lượng và đơn giá
là số hợp lệ, lớn hơn 0.
Công thức: Tổng tiền = Số lượng × Đơn giá.

Bước 3: Phân loại đơn hàng:
- HỢP LỆ: Đầy đủ thông tin và dữ liệu chính xác.
- CẦN BỔ SUNG: Thiếu thông tin khách hàng.
- CẦN KIỂM TRA: Dữ liệu sai định dạng hoặc bất thường.

Ràng buộc:
- Không tự suy đoán hoặc điền dữ liệu còn thiếu.
- Không tính tiền nếu dữ liệu không hợp lệ.
- Giữ nguyên kết quả của từng bước khi chuyển tiếp.
- Nếu đầu vào mâu thuẫn, phải thông báo rõ.
- Không bỏ qua bất kỳ lỗi nào.

Đầu ra gồm: Thông tin đơn hàng, kết quả kiểm tra,
tổng tiền, trạng thái và hướng xử lý.
Trình bày bằng tiếng Việt, rõ ràng, ngắn gọn.
```

## **2. Bảng so sánh Trade-off**

| Tiêu chí               | Giải pháp 1 (Đơn giản) | Giải pháp 2 (Chi tiết) |
| ---------------------- | ---------------------- | ---------------------- |
| Độ dễ hiểu             | Cao                    | Trung bình             |
| Tốn token              | Ít                     | Nhiều hơn              |
| Tốc độ xử lý           | Nhanh                  | Chậm hơn đôi chút      |
| Độ chính xác           | Trung bình             | Cao                    |
| Chặn lỗi biên          | Trung bình             | Rất tốt                |
| Kiểm soát đầu ra       | Thấp                   | Cao                    |
| Xử lý đứt gãy ngữ cảnh | Hạn chế                | Tốt                    |
| Khả năng mở rộng       | Trung bình             | Cao                    |

**Nhận xét:** Giải pháp 1 phù hợp với công việc đơn giản, ít dữ liệu. Giải pháp 2 tốn nhiều token hơn nhưng kiểm soát quy trình tốt, hạn chế AI tự suy đoán và bỏ sót lỗi.

## **3. Lựa chọn giải pháp tối ưu**

Em lựa chọn **Giải pháp 2** vì có quy trình xử lý theo từng giai đoạn, điều kiện rõ ràng và khả năng kiểm soát lỗi tốt hơn. Đặc biệt, việc duy trì kết quả giữa các bước giúp hạn chế đứt gãy ngữ cảnh.

## **4. Kết quả chạy thử**

**Input:**

- Khách hàng: Nguyễn Văn An.
- Số điện thoại: 0901234567.
- Địa chỉ: Để trống.
- Sản phẩm: Chuột không dây.
- Số lượng: 2.
- Đơn giá: 150.000 đồng.

**Output AI:**

```
1. KIỂM TRA:
- Họ tên: Hợp lệ.
- Số điện thoại: Đã cung cấp.
- Địa chỉ: Thiếu.
- Sản phẩm: Chuột không dây.
- Số lượng: 2 (Hợp lệ).
- Đơn giá: 150.000 đồng (Hợp lệ).

2. TÍNH TOÁN:
Tổng tiền = 2 × 150.000
          = 300.000 đồng.

3. PHÂN LOẠI:
Trạng thái: CẦN BỔ SUNG.

Lý do: Khách hàng chưa cung cấp địa chỉ.

Hướng xử lý: Yêu cầu khách hàng bổ sung
địa chỉ trước khi xác nhận đơn hàng.
```

## **5. Kết luận**

Qua so sánh, Giải pháp 2 tối ưu hơn đối với quy trình xử lý đơn hàng thực tế. Mặc dù tiêu tốn nhiều token hơn, phương án này giúp tăng độ chính xác, kiểm soát lỗi và duy trì tính nhất quán giữa các bước. Qua đó, em hiểu được tầm quan trọng của việc thiết kế Prompt Chaining có logic và điều kiện rõ ràng trước khi triển khai tự động hóa bằng code.
