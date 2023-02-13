# 1. Layout là gì?
- Layout là thành phần định nghĩa cấu trúc giao diện người dùng hay nói cách khác là thành phần quyết định đến giao diện của một màn hình trong ứng dụng Android.
- Layout hỗ trợ việc căn chỉnh các widget (Ví dụ: TextView, Button, hay EditText…) như chúng ta thấy trong các ứng dụng Android.
# 2. Các loại layout trong Android.
## 2.1: RelativeLayout
### a) Định nghĩa
- RelativeLayout là một ViewGroup có hiển thị các View con ở các vị trí tương đối.
- Vị trí của mỗi View có thể được quy định liên quan đến các View anh em (như bên trái của hoặc bên dưới một View khác) hoặc ở các vị trí tương đối với khu vực cha RelativeLayout(chẳng hạn như sắp xếp ngay phía dưới, bên trái hoặc trung tâm).
### b) Thuộc tính
- Các View con khi đã định vị xong trong RelativeLayout, giả sử coi như tất cả các View con nằm vừa trong một đường biên chữ nhật, thì cả khối các View con này có thể dịch chuyển tới những vị trí nhất định trong RelativeLayout bằng thuộc tính: `android:gravity`, nó nhận các giá trị (có thể tổ hợp lại với ký hiệu `|` )
    - center: Căn ở giữa
    - top: Ở phần trên
    - bottom: Phần dưới
    - center_horizontal: Ở giữa theo chiều ngang
    - center_vertical: Ở giữa theo chiều đứng
    - left: Theo cạnh trái
    - right: Theo cạnh phải
    - bottom: Cạnh dưới
### c) Định vị view con bằng view cha
- `android:layout_alignParentBottom`: true căn thẳng cạnh dưới view con với cạnh dưới View cha
- `android:layout_alignParentLeft`: true căn thẳng cạnh trái view con với cạnh trái View cha
- `android:layout_alignParentRight`:	true căn thẳng cạnh phải view con với cạnh phải View cha
- `android:layout_alignParentTop`:	true căn thẳng cạnh trên view con với cạnh trên View cha
- `android:layout_centerInParent`:	true căn view con vào giữa View cha
- `android:layout_centerHorizontal`:	true căn view con vào giữa View cha theo chiều ngang
- `android:layout_centerVertical`:	true căn view con vào giữa View cha theo chiều đứng
### d) Định vị các view con với nhau bằng thuộc tính liên hệ với nhau
- `android:layout_alignTop` – Chỉ định đỉnh của thành phần này sẽ được canh theo đỉnh của thành phần gọi đến bằng ID.
- `android:layout_alignBottom` – Chỉ định đáy của thành phần này sẽ được canh theo đáy của thành phần gọi đến bằng ID.
- `android:layout_alignStart` – Chỉ định cạnh start của thành phần này sẽ được canh theo cạnh start của thành phần gọi đến bằng ID.
- `android:layout_alignEnd` – Chỉ định cạnh end của thành phần này sẽ được canh theo cạnh end của thành phần gọi đến bằng ID.
- `android:layout_alignBaseline` – Chỉ định baseline của thành phần này sẽ được canh theo baseline của thành phần gọi đến bằng ID. Baseline này bạn không nhìn thấy được, dùng để canh chỉnh cho text hiển thị bên trong widget, do đó sẽ hữu dụng khi canh chỉnh các TextView với nhau).
- `android:layout_above` – Chỉ định thành phần này sẽ nằm ở trên so với thành phần gọi đến bằng ID.
- `android:layout_below` – Chỉ định thành phần này sẽ nằm dưới so với thành phần gọi đến bằng ID.
- `android:layout_toStartOf` – Chỉ định thành phần này sẽ nằm bên phía start so với thành phần gọi đến bằng ID.
- `android:layout_toEndOf` – Chỉ định thành phần này sẽ nằm bên phía end so với thành phần gọi đến bằng ID.
- `android:layout_toLeftOf` – Chỉ định thành phần này sẽ nằm bên phía trái so với thành phần gọi đến bằng ID.
- `android:layout_toRightOf` – Chỉ định thành phần này sẽ nằm bên phía phải so với thành phần gọi đến bằng ID.
## 2.2: LinearLayout
### a) Định nghĩa
- LinearLayout là loại layout sẽ sắp xếp các view theo chiều dọc hoặc ngang theo thứ tự của các view.
- Đây là ViewGroup sẽ giúp các bạn sắp xếp các view con chứa bên trong theo dạng hàng ngay hoặc hàng dọc với nhau.
### b) Thuộc Tính Lực Hấp Dẫn (Gravity)
- Mặc định thì các thành phần con bên trong LinearLayout sẽ được “hút” về start-top theo “lực hấp dẫn” mặc định
- Thuộc tính android:gravity để căn chỉnh các View nằm ở vị trí nào trong LinearLayout, nó nhận các giá trị (có thể tổ hợp lại với ký hiệu |)
- Các lệnh phổ biến:
    - center: Căn ở giữa
    - top: Ở phần trên
    - bottom: Phần dưới
    - center_horizontal:	Ở giữa theo chiều ngang
    - center_vertical:	Ở giữa theo chiều đứng
    - left:	Theo cạnh trái
    - right:	Theo cạnh phải
    bottom	Cạnh dưới
### c) Thuộc Tính Trọng Số (Weight)
- Các View con trong LinearLayout có thể gán cho nó một giá trị trọng số bằng thuộc tính `android:layout_weight`
- Nếu View không gán giá trị này coi như nó có trọng số bằng không.
- Trường hợp LinearLayout không sử dụng đến thuộc tính `android:weightSum`.
- Khi chúng ta muốn các view tự động full màn hình thì sử dụng `android:weightSum`.
# 3. View
## 3.1: Các view hiển thị
### a) TextView
- Đây là `View` mà chúng ta sử dụng trong ví dụ trên. Công việc chính của `TextView` là hiển thị văn bản trên màn hình một ứng dụng Android. Mặc dù điều này có vẻ như là một nhiệm vụ đơn giản, nhưng lớp `TextView` chứa logic phức tạp cho phép nó hiển thị mã đánh dấu, siêu liên kết, số điện thoại, email và các chức năng hữu ích khác.
- Cú pháp:
``` cpp
<TextView
     attribute1="value"
     attribute2="value"
     attribute3="value"
... />
```
- `android:text`: xác định văn bản sẽ hiển thị lên `TextView`.
- `android:textColor`: xác định màu chữ của `TextView`.
- `android:textSize`: xác định kích thước chữ của `TextView`.
- `android:textStyle`: xác định kiểu chữ `TextView`, có 3 giá trị là `normal` (thông thường), `bold` (in đậm), `ilalic` (nghiêng).
- `android:drawableLeft`: xác định drawable nằm bên trái văn bản.
- `android:drawableRight`: xác định drawable nằm bên phải văn bản.
- `android:drawableTop`: xác định drawable nằm bên trên văn bản.
- `android:drawableLeft`: xác định drawable nằm bên dưới văn bản.
### b) ImageView
- Như tên của nó, `ImageView` được thiết kế đặc biệt để hiển thị hình ảnh trên màn hình. Điều này có thể được sử dụng để hiển thị các tài nguyên được lưu trữ trong ứng dụng hay để hiển thị hình ảnh được tải xuống từ internet.
- Một số thuộc tính:
    - `android:id`: xác định id.
    - `android:src`: xác định nguồn hình ảnh hoặc `drawable`.
    - `android:scaleType`: kiểu hiển thị hình ảnh của `ImageView`.
        - Có các giá trị: fitCenter, fitStart, fitEnd, center, centerCrop, centerInside, matrix.
- Để gán hình ảnh động trong Java, sử dụng các phương thức sau:
    - Nếu nguồn là bitmap: void setImageBitmap(Bitmap bm).
    - Nếu nguồn là id của hình ảnh nằm trong thư mục drawable: void setImageResource(@DrawableRes int resId).
    - Nếu nguồn là drawable: void setImageDrawable(@Nullable Drawable drawable).
## 3.2: Control nhập liệu
### a) Định nghĩa
- Một số đối tượng `View` được sử dụng không chỉ để hiển thị nội dung cho người dùng. Đôi khi bạn cần phải có một số trường nhập liệu để kiểm soát các ứng dụng của bạn. May mắn thay, Android cung cấp một số lớp con đặc biệt của View cho mục đích này.
### b) Button
- Lớp `Button` là một trong các control cơ bản nhất có sẵn trong ứng dụng. Nó lắng nghe sự kiện nhấp của người dùng và gọi một phương thức trong code của bạn vì vậy mà bạn có thể phản hồi một cách thích hợp.
- 1 vài thuộc tính co bản tương tự như trong `TextView`
- Để thực hiện những khối lệnh khi nhấp chuột vào Button làm như sau:
``` cpp
Button btnClick = (Button)findViewById(R.id.btn_click);
btnClick.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
    }
});
```
### c) Switch và CheckBox
- Các lớp `Switch` và `CheckBox` có một trạng thái hoạt động và không hoạt động có thể được bật tắt. Điều này rất hữu ích cho việc thay đổi các cài đặt trong ứng dụng. Các phiên bản tương thích với Material Design có sẵn thông qua thư viện hỗ trợ AppCompat.
### d) EditText
- Lớp con này của `View` là một sự mở rộng của lớp `TextView` và cho phép người dùng cập nhật văn bản thông qua một bàn phím.
- Cú pháp:
``` cpp
<EditText
     attribute1="value"
     attribute2="value"
     attribute3="value"
... />
```
- `android:text`: xác định văn bản hiển thị lên EditText.
- `android:textColor`: xác định màu của text.
- `android:textSize`: xác định kích thước của text.
- `android:textStyle`: xác định kiểu của văn bản gồm các giá trị italic (nghiêng), bold (in đậm), normal (kiểu thường).
- `android:inputType`: xác định phương thức nhập của Edittext.
    - Có các giá trị như sau: text, number, textPassword, phone, textUrl, …
- Để lấy text của EditText trong Java làm như sau:
    - Lấy EditText thông qua id trong file XML.
    - Sử dụng phương thức getText() của EditText để lấy chuỗi.
``` cpp
EditText edtMessage = (TextView)findViewById(R.id.edt_message);
String value = edtMessage.getText().toString();
```
## 3.3: Adapter View
### a) Định nghĩa
- Trong khi mỗi ví dụ `View` ở trên là những phần tử đơn lẻ, nhưng đôi khi bạn muốn hiển thị một tập hợp các phần tử. Các lớp `View` này yêu cầu sử dụng một Adapter để xử lý việc hiển thị giao diện người dùng thích hợp cho mỗi phần tử trong một bộ sưu tập.
### b) ListView
- Lớp `ListView` được sử dụng để hiển thị một tập hợp các phần tử trong một `View` dài, một cột, có thể cuộn. Mỗi mục phần tử riêng lẻ có thể được chọn để hiển thị chi tiết hoặc thực hiện một hành động liên quan đến phần tử đó.
### c) GridView
- Tương tự như lớp `ListView`, lớp `GridView` nhận một `Adapter` và hiển thị các phần tử trên nhiều cột trên màn hình.
### d) Spinner
- Nó chấp nhận một `Adapter` và hiển thị các phần tử trong trình đơn thả xuống khi `Spinner` được nhấp vào để cho một phần tử có thể được lựa chọn bởi người dùng.
## 3.4: Thuộc tính của View
### a) layout_height
- Thuộc tính `layout_height` quy định chiều cao của View và có các giá trị như sau:
    - match_parent: chiều cao của View sẽ bằng đúng chiều cao của phần tử cha chứa nó.
    - wrap_content: chiều cao của View phụ thuộc vào content của View.
    - Giá trị xác định: đơn vị chiều cao của View như dp, px, in, mm, sp, ...
### b) layout_width
- Thuộc tính layout_width quy định chiều rộng của View và có các giá trị như sau:
    - match_width: chiều rộng của View sẽ bằng đúng chiều rộng của phần tử cha chứa nó.
    - wrap_content: chiều rộng của View phụ thuộc vào content của View.
    - Giá trị xác định: đơn vị chiều rộng của View như dp, px, in, mm, sp, ...
### c) id
- Thuộc tính `id` xác định `id` của `View`, được khai báo ở file định nghĩa giao diện XML và sử dụng lại trong code Java để ánh xạ đối tượng, tìm kiếm các `View` trong code Java khi cần.
### d) background
- Thuộc tính `background` xác định màu nền của `View`.
- vd:
``` cpp 
android:background="#ffffff" // white color 
```
### e) margin và padding
- `margin`: là khoảng cách từ các cạnh của View hiện tại tới các View khác.
- `padding`: là khoảng cách từ các cạnh của View tới phần nội dung bên trong.