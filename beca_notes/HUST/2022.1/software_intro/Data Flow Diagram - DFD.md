> [!info] Data Flow Diagram
> Biểu diễn một cách linh hoạt  các thực thể ngoài, các chức năng, luồng dữ liệu và các kho dữ liệu

* DFD là một trong những công cụ hữu hiệu của giai đoạn phân tích yêu cầu. 

### Xây dựng DFD theo các mức cấp bậc
#### Sơ đồ ngữ cảnh
* Sơ đồ mức **cao nhất**.
* Cho ra một cái nhìn tổng quát về hệ thống trong môi trường tồn tại.
* Chỉ có một tiến trình **duy nhất**, các tác nhân và các luồng dữ liệu.
* **Không có kho dữ liệu.**

#### Sơ đồ mức 0
* Sơ đồ phân rã từ sơ đồ ngữ cảnh.
* Mô tả hệ thống chi tiết hơn.
* Các tiến trình được trình bày là các mục chức năng chính của hệ thống

#### Sơ đồ mức i
* Là sơ đồ được phân rã từ mức i-1
* Mỗi sơ đồ phân rã mức sau là sự chi tiết hoá của một tiến trình mức trước.
* Quá trình phân ra sẽ dừng lại khi đạt được sơ đồ luồng dữ liệu sơ cấp.
> [!info] sơ đồ luồng dữ liệu sơ cấp
> Khi trong sơ đồ, một tiến trình là một phép tính toán hay thao tác dữ liệu đơn giản, khi mỗi luồng dữ liệu không cần chia nhỏ nữa.

* Mỗi biểu đồ DFD cũng đi kèm với các mô tả chi tiết về ý nghĩa các luồng dữ liệu và các bước thực hiện của chức năng xử lý.
* DFD cũng cung cấp thông tin về đầu ra và đầu vào của mỗi thực thể và chính quá trình.

![[Pasted image 20221205124045.png]]