# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn


- Mã học viên theo lớp: 2A202603247
- Ngày / CVAT local: 12/11/2026
- Công cụ đã dùng: CVAT local, Python, VS Code, GitHub


## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |


## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `medium_instance/000000458325.jpg`, phía trái dưới frame, object là car.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi giữ mask theo cạnh thân xe và không kéo qua nền; chỉ phủ phần vật thật sự nhìn thấy, không bao gồm bóng, nền hoặc khoảng trống xung quanh.
- Tôi chọn `car` vì phần thân xe có dạng rõ và không lẫn với bóng hoặc mặt đường.

## 3. Một lỗi tôi tìm thấy và sửa


- Task/ảnh/vùng: easy_semantic, ảnh 817bca71-00000000, ranh giữa `road` và `sidewalk`.
- Lỗi thuộc loại: biên
- Bằng chứng tôi nhìn thấy: Ở vùng cạnh đường, ranh road–sidewalk bị ăn vào vùng sidewalk vì brush quá rộng; hình ảnh cho thấy phần nền phải là road nhưng đã nằm trong sidewalk.
- Quy tắc và hành động sửa: Theo quy tắc semantic, road và sidewalk là hai lớp riêng; tôi dùng brush nhỏ và dời lại biên theo góc mặt đường, giữ phần lát gạch/đi bộ đúng với khu vực thực tế. Sau đó tôi Save lại và export ZIP mới.
- Sau sửa đã Save và export lại chưa? Có, tôi đã Save và export lại file `easy_semantic.zip`.


## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 000000373353 / ở medium_instance | Xe car vàng bị che bởi một người ở trước mặt, nên tôi phải lựa chọn giữa xem đó là một object hay chia thành hai phần riêng | Cách hiểu thứ nhất là giữ nguyên chiếc xe là một object vì vật thể vẫn là cùng một xe dù bị che. Cách hiểu thứ hai là chia ra thành 2 phần do bị cắt bởi người ở trước. | Tôi đã quyết định giữ như một object car duy nhất ở phần nhìn thấy của xe, nhưng tôi vẫn chưa chắc vì vùng bị che có thể khiến người chấm hiểu là hai phần tách rời. Tôi muốn hỏi coach liệu khi một vật bị che tạo thành nhiều mảng nhìn thấy thì vẫn nên giữ là một instance hay phải tách thành nhiều instance. |
| 7ee6d192-89e2408b / ở easy_sematic | Phần road trải dài và có nhiều xe car phía sau; tôi chưa chắc có nên vẽ mask road đè lên các xe ở xa và các vùng mờ hay phải bỏ qua những phần đó | Cách hiểu thứ nhất là road cần phủ hết phần mặt đường nhìn thấy, kể cả những vị trí có xe đi qua. Cách hiểu thứ hai là chỉ nên vẽ road ở vùng không có vật cản, còn các xe và vùng mờ nên tách riêng. | Tôi đã quyết định vẽ phần road ở vùng nhìn thấy gần, và bỏ các chi tiết rõ ràng như xe ở gần, nhưng vẫn có cảm giác các xe ở xa mờ có thể bị phủ nhầm vào road. Tôi vẫn muốn kiểm tra lại theo quy tắc: road là lớp nền, chỉ phủ phần mặt đường thật sự, không nên lấn sang vehicle. |
| 000000460147 / ở hard_panoptic | Nhiều xe car nằm trên một xe truck, nên tôi chưa chắc có nên gán toàn bộ vùng đó là truck hay phải giữ xe car ở trên như một instance riêng | Cách hiểu thứ nhất là xe truck là object lớn ở dưới, nên những vùng xe car nằm trên nó vẫn thuộc truck nếu chúng là cùng một mảng không tách rõ. Cách hiểu thứ hai là các xe car ở trên phải được gán riêng vì là object khác. | Tôi đã chọn gán vùng dưới dạng truck ở phần lớn và giữ các xe trên còn lại theo lớp vehicle riêng nếu có hình dạng rõ. Tuy nhiên, tôi vẫn chưa chắc khi các vật chồng lên nhau như vậy, nên muốn xin coach xác nhận cách quy định đối với “vật nằm trên vật” trong panoptic. |
