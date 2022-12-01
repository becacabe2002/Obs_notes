## I. Mô hình tổ chức bộ nhớ
* Bộ nhớ sơ cấp:
  - Các thiết bị nhớ mà CPU mà máy tính có thể thao tác trực tiếp (Bộ nhớ chính, bộ nhớ đệm, cache...)
  - Truy cập nhanh, nhưng giới hạn về dung lượng.

* Bộ nhớ thứ cấp:
  - CPU không xử lý được trực tiếp mà phải sao chép sang bộ nhớ sơ cấp để xử lý (Đĩa từ, đĩa quang, băng từ)
  - Truy cập chậm hơn nhưng dung lượng lớn + chi phí rẻ hơn

### Bộ nhớ ngoài (bộ nhớ thứ cấp)

- Được chia thành các **khối vật lý (sector)** (512-4096 byte) được đánh địa chỉ khối (**địa chỉ tuyệt đối**)

- 1 tệp = 1 hoặc nhiều khối, mỗi khối chứa 1 hoặc nhiều bản ghi.

- Thao tác với dữ liệu của tệp thông qua địa chỉ tuyệt đối của các khối.

- Các bản ghi đều có địa chỉ:
  + Địa chỉ tuyệt đối của ***byte đầu tiên***
  + Địa chỉ khối, số byte tính từ đầu khối đến vị trí đầu bản ghi

- Địa chỉ của các bản ghi/khối được lưu ở 1 tệp, dữ liệu được truy cập = **con trỏ** (pointer)

## II. Tổ chức tệp đống (Heap file)
> Là tổ chức lưu trữ đơn giản nhất, các bản ghi được **lưu trữ kế tiếp** nhau trong các khối, **không theo một thứ tự đặc biệt** nào và **không có một tổ chức đặc biệt** nào đối với các khối.

![Image](https://static.javatpoint.com/dbms/images/dbms-heap-file-organization.png)

![Img](../attachments/C7-heap.png)

### Các thao tác

* **Tìm kiếm một bản ghi**: tìm kiếm một bản ghi có giá trị cho trước bằng việc quét toàn bộ tệp

* **Thêm một bản ghi**: thêm bản ghi mới sau bản ghi cuối cùng

* **Xoá một bản ghi**:
  - Bao gồm cả thao tác tìm kiếm
  - Nếu có bản ghi cần xoá -> đánh dấu bản ghi là xoá
  => Hệ thống cần tổ chức lại đĩa định kỳ

* **Sửa một bản ghi**: tìm bản ghi rồi sửa một hay nhiều trường

<mark style='background:#90EE90'>**LỢI THẾ**</mark>
- Thiết kế đơn giản nhất, giá lưu trữ rẻ
- Phù hợp cho các thao tác chèn hàng loạt và các tệp/bảng nhỏ

<mark style='background: pink'>**BẤT LỢI**</mark>
+ Các bản ghi nằm rải rác trong bộ nhớ và chúng được sử dụng không hiệu quả -> Làm tăng kích thước bộ nhớ
+ Cần có quản lý bộ nhớ thích hợp
+ Không thích hợp cho bảng lớn

## III. Tổ chức tệp băm (Hash file)

* ***Hàm băm***: &h(x)= x mod k&

![Image](https://static.javatpoint.com/dbms/images/dbms-hash-file-organization.png)

![Img](../attachments/C7-hash.png)

* Tổ chức tệp dữ liệu:
  - Phân chia các record *vào các cụm*
  - Mỗi cụm gồm một hoặc nhiều khối
  - Mỗi khối chứa *số lượng record cố định*
  - Tổ chức lưu trữ dữ liệu trong mỗi cụm áp dụng theo *tổ chức đống*

* ***Tiêu chí chọn hàm băm***: phân bố các bản ghi tương đối đồng đều theo các cụm

### Các thao tác

* **Tìm kiếm một bản ghi**: 
  - Tìm bản ghi có khoá x bằng việc tính h(x) sẽ được cụm chứa bản ghi.
  - Khi có được cụm chứa bản ghi, tiến hành tìm kiếm theo tổ chức đống

* **Thêm một bản ghi**: thêm bản ghi có giá trị khoá là x
  - Nếu trong tệp đã có bản ghi có khoá x -> bản ghi mới sai (khoá là duy nhất)
  - Nếu trong tệp không có bản ghi, bản ghi được thêm vào khối còn chỗ trống đầu tiên trong cụm. Nếu hết chỗ -> tạo khối mới.

* **Xoá một bản ghi**: tìm kiếm bản ghi rồi xoá

* **Sửa đổi một bản ghi**:
  - Nếu trường cần sửa có tham gia vào trong khoá: loại bỏ bản ghi này - thêm mới 1 bản ghi (có thể thuộc vào 1 cụm khác)
  - Nếu trường cần sửa không thuộc khoá: tìm kiếm rồi sửa. Nếu bản ghi không tồn tại thì xem như có lỗi.

## IV. Tổ chức tệp chỉ dẫn (Indexed file)
* Các khoá của bản ghi được sắp xếp tăng dần

* Tệp chỉ dẫn được tạo bằng cách chọn các trị khoá trong các bản ghi

* Tệp chỉ dẫn (k,d) - `k` là giá trị khoá của bản ghi đầu tiên. - `d` là địa chỉ khối (con trỏ khối)

![Img](../attachments/C7-index.png)

### Tìm kiếm trên tệp chỉ dẫn
* Giá trị khoá k -> cần tìm bản ghi (k_m, d) trong tệp chỉ dẫn nếu k_m <= k_i và:
  * hoặc (k_m, d) là bản ghi cuối cùng của tệp chỉ dẫn
  * hoặc (k_{m+1}, d') thoả mãn k_i < k_{m+1}

-> k_m phủ k_i

* Tìm kiếm: **tuần tự** hoặc **nhị phân**

### Các thao tác

* **Tìm kiếm một bản ghi**:

* **Thêm một bản ghi**: xác định khối i sẽ chứa bản ghi đó.
  * Khối i còn chỗ -> đặt bản ghi vào đúng cgỗ theo thứ tự sắp xếp của khoá, dồn các toa bản ghi đằng sau.

  * Khối i hết chỗ -> Đẩy bản ghi cuối cùng trong khối sang làm bản ghi đầu tiên của khối tiếp theo i+1. Sửa bản ghi chỉ dẫn tương ứng.

  * Nếu bản ghi mới này có giá trị khoá lớn hơn tất cả mọi khoá trong tệp dữ liệu chính và không còn chỗ thì tạo thêm 1 khối mới.

* **Xoá một bản ghi** 
  * Giống như thêm một bản ghi, nếu xoá mà tạo thành 1 khối rỗng
  -> Có thể loại bỏ cả khối đó.

* **Sửa một bản ghi**
  * Sử dụng tìm kiếm để xác định bản ghi cần sửa
 
  * Nếu các trường cần sửa ko p là khoá thì sửa bth.
  * Nếu các trường cần sửa tham gia vào khoá thì quá trình sửa sẽ tốn thêm thời gian. (+ thêm bản ghi + xoá bản ghi) 

## V. Cây cân bằng (Balanced-trees)
* Được tổ chức theo **cây cấp m**

  * Gốc của cây là một nút lá hoặc một nút lá hoặc ít nhất có hai con

  * Mỗi nút (trử gốc nút và nút lá) cò từ **m/2 -> m** con

  * Mỗi đường đi từ nút gốc đến bất kì nút lá nào đều có **độ dài bằng nhau**.

![Tree Image](../attachments/C7-tree.png)

* Mỗi nút có dạng (p0, k1, p1, k2, ..., kn, pn) 
  * p_i (i = 1..n) - con trỏ tới khối i của nút có **k_i là khoá đầu tiên của khối đó.**
  * Các khoá k trong một nút được sắp xếp theo thứ tự tăng dần.

* Mọi khoá trong cây con, trỏ bởi con trỏ p0 đều nhỏ hơn k1;
* Mọi khoá trong cây con, trỏ bởi p_i đều nhỏ hơn k_{i+1}
* Moji khoá trong cây con, trỏ bởi p_n đều lớn hơn k_m.

### Các thao tác

* **Tìm kiếm một bản ghi**: xác định đường dẫn từ nút gốc tới nút lá chứa bản ghi này

* **Thêm một bản ghi**:
  * tìm kiếm bản ghi 
  * Còn chỗ, thêm như bth
  * Hết chỗ, tạo thêm nút lá mới, chuyển nửa dữ liệu của nút lá hiện tại sang nút mới, sau đó thêm bản ghi mới này vào vị trí phù hợp nút lá hiện tại hoặc nút lá mới tạo.
  * Rất có khả năng "đụng chạm" đến nút cha, nút gốc

* **Loại bỏ một bản ghi**:
  * Tìm kiếm bản ghi -> tìm ra nút L có thể chứa bản ghi đó.
  * Rất có khả năng "động chạm" đến nút cha, nút gốc



