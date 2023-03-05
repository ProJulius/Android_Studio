# 1. Giới thiệu Activity trong Android Studio
- Lớp `Activity` là thành phần quan trọng nhất của ứng dụng `Android`, cách mà chúng hoạt động tạo thành nền tảng cơ bản của mô hình lập trình ứng dụng. `Android` khởi chạy một ứng dụng thông thường bằng kích hoạt một `Activity` tương ứng với vòng đời cụ thể của nó trong quá trình hoạt động.
- Thường một `Activity` cung cấp một của sổ, ở đó ứng dụng sẽ dựng các thành phần UI (User Interface - giao diện người dùng). Mặc định cửa sổ này có thể lấp đầy mà hình thiết bị, nhỏ hơn hoặc nổi phía trên các cửa sổ khác. Hầu hết các ứng dụng đều sử dụng nhiều màn hình khác nhau, có nghĩa nó sẽ phải có nhiều `Activity` khác nhau. Khi một `Activity` chỉ định là `Main Activity`, nó sẽ là màn hình đầu tiên khi khởi chạy ứng dụng. `Activity` này có thể gọi và kích hoạt một `Activity` khác.
# 2. Vòng đời Activity
## 2.1. Sơ đồ
![](https://imgur.com/OtVeVN6.png)
## 2.2. Mô tả sơ đồ
- Sơ đồ bắt đầu từ khi `Activity launched`, tức là khi Activity được kích hoạt, và được hệ thống đẩy vào BackStack. Sau khi kích hoạt, lần lượt các callback `onCreate()`, `onStart()`, `onResume()` sẽ được hệ thống gọi đến. Sau khi gọi đến các callback trên, thì Activity mới chính thức được xem là đang chạy (Activity running).
- Lúc này, nếu có bất kỳ Activity nào khác chiếm quyền hiển thị, thì Activity hiện tại sẽ rơi vào trạng thái `onPause()`.
    - Nếu sự hiển thị của Activity khác làm cho Activity mà chúng ta đang nói đến vẫn còn nhìn  thì đang ở trạng thái `onPause()`(Mở một màn hình mới đè lên màn hình cũ nhưng vẫn thấy màn hình cũ.)
    - Nếu sự hiển thị của Activity khác làm cho Activity mà chúng ta đang nói đến không còn nhìn thấy nữa thì `onStop()` sẽ được gọi ngay sau đó.(Mở một màn hình mới, tắt màn hình cũ.)
- Khi ở trạng thái `onPause()` mà người dùng sau đó quay về lại Activity cũ, thì `onResume()` được gọi. 
- Khi ở trạng thái `onStop()`mà người dùng sau đó quay về lại Activity cũ, thì `onRestart()` được gọi. 
- Trong cả hai trường hợp Activity rơi vào `onPause()` hoặc `onStop()`, nó sẽ rất dễ bị hệ thống thu hồi (tức là bị hủy) để giải phóng tài nguyên, khi này nếu quay lại Activity cũ, `onCreate()` sẽ được gọi chứ không phải `onResume()` hay `onRestart()`. Và cuối cùng, nếu một Activity bị hủy một cách có chủ đích, chẳng hạn như người dùng nhấn nút Back ở System Bar, hay hàm finish() được gọi,… thì `onDestroy()` sẽ được kích hoạt và Activity kết thúc vòng đời của nó.
## 2.3. Các trạng thái chính trong vòng đời Activity
### **Runing**
-> Khi Activity được kích hoạt, và được hệ thống để vào BackStack, nó sẽ bước vào trạng thái active. Với trạng thái active, người dùng hoàn toàn có thể nhìn thấy và tương tác với Activity của ứng dụng.
### **Pause**
-> Trạng thái này khá đặc biệt. Trạng thái tạm dừng. Như bạn đã làm quen trên kia, trạng thái này xảy ra khi mà Activity của bạn vẫn đang chạy, người dùng vẫn nhìn thấy, nhưng Activity khi này lại bị che một phần bởi một thành phần nào đó. Chẳng hạn như khi bị một dialog đè lên. Cái sự che Activity này không phải hoàn toàn. Chính vì vậy mà Activity đó tuy được người dùng nhìn thấy nhưng không tương tác được.
### **Stop**
-> Trạng thái này khá giống với trạng thái tạm dừng trên kia. Nhưng khi này Activity bị che khuất hoàn toàn bởi một thành phần giao diện nào đó, hoặc bởi một ứng dụng khác. Và tất nhiên lúc này người dùng không thể nhìn thấy Activity của bạn được nữa.
Hành động mà khi người dùng nhấn nút Home ở System Bar để đưa ứng dụng của bạn về background, cũng khiến Activity đang hiển thị trong ứng dụng rơi vào trạng thái dừng này.
### **Dead**
-> Nếu Activity được lấy ra khỏi BackStack, chúng sẽ bị hủy và rơi vào trạng thái này. Trường hợp này xảy ra khi user nhấn nút Back ở System Bar để thoát một Activity. Hoặc lời gọi hàm finish() từ một Activity để “kill chính nó”. Cũng có khi ứng dụng ở trạng thái background quá lâu, hệ thống có thể sẽ thu hồi tài nguyên bằng cách dừng hẳn các Activity trong ứng dụng, làm cho tất cả các Activity đều vào trạng thái này.
Khi vào trạng thái dead, Activity sẽ kết thúc vòng đời của nó.
## 2.4. Làm quen với các callback
### **onCreate()**
-> Hàm này được gọi khá sớm, ngay khi activity được kích hoạt và thầm chí người còn chưa thấy gì cả thì callback này đã đc gọi rồi. Ngoài ra thì bạn nên biết là callback này chỉ được gọi một lần duy nhất khi Activity được khởi tạo. Nó có thể được gọi lại nếu hệ thống xóa Activity này đi để lấy lại tài nguyên của hệ thống, nhưng rất hiếm khi xảy ra. Và nó còn có thể được gọi lại nếu bạn xoay màn hình (ngang/dọc).
Do đặc tính được gọi khá sớm và chỉ được gọi một lần duy nhất trong vòng đời của nó như vậy, nên bạn sẽ tận dụng để load giao diện cho Activity ở giai đoạn này, thông qua phương thức setContentView().
Ngoài giao diện ra, bạn có thể khởi tạo các logic nào đó chỉ chạy một lần ban đầu, như các lời gọi API, load database, tạo item list, tạo Navigation Drawer, và nhiều logic khác.
### **onStart()**
-> Sau khi gọi đến onCreate(), hệ thống sẽ gọi đến onStart(). Hoặc hệ thống cũng sẽ gọi lại onStart() sau khi gọi onRestart() nếu trước đó nó bị che khuất bởi Activity nào khác (một màn hình khác hoặc một ứng dụng khác) che hoàn toàn và rơi vào onStop().
Khi hệ thống gọi đến callback này thì Activity được nhìn thấy bởi người dùng và nhưng chưa tương tác được. Bởi đặc tính này mà onStart() ít được dùng đến.
### **onResume()**
-> Khi hệ thống gọi đến callback này thì bạn yên tâm rằng người dùng đã nhìn thấy và đã tương tác được với giao diện.
onResume() được gọi khi Activity được khởi tạo rồi và bước qua onStart() trên kia. Hoặc khi Activity bị một giao diện nào khác che đi một phần (hoặc toàn phần), rồi sau đó quay lại Activity hiện tại. Bạn có thể thấy rằng callback này được gọi rất nhiều lần trong một vòng đời của nó.
Chính đặc điểm này của onResume() mà bạn có thể tận dụng để quay lại tác vụ mà người dùng đang bị dang dở khi onPause() (được nói đến dưới đây) được gọi.
Chẳng hạn như bạn đang soạn nội dung cho TourNote, mà có cuộc gọi đến, bạn sẽ lưu tạm nội dung này khi callback onPause(), để rồi khi onResume() được gọi lại sau đó khi người dùng kết thúc cuộc gọi và quay lại TourNote, bạn sẽ khôi phục nội dung đó để người dùng tiếp tục sử dụng TourNote như chưa có bất kỳ gián đoạn nào.
### **onPause()**
-> Thông thường nếu có một thành phần nào đó che Activity hiện tại mà người dùng vẫn nhìn thấy Activity đó (nhìn thấy chứ không tương tác được). Chẳng hạn một popup hiện lên trên Activity. Thì onPause() của Activity sẽ được gọi. Sau này khi người dùng quay lại Activity thì onResume() sẽ được gọi.
Bạn có thể tưởng tượng rằng onPause() cũng sẽ được gọi khá nhiều lần trong một vòng đời Activity. Theo như Google thì onPause() được gọi đến khá nhanh, nếu bạn muốn lưu trữ dữ liệu như mình nói trên kia, thì nên lưu những gì nhanh gọn lẹ thôi. Nếu bạn muốn lưu trữ các dữ liệu nặng, hoặc gọi API kết nối server chỗ này, nhiều khả năng ứng dụng sẽ không kịp thực hiện. Do đó, thay vì làm các thao tác nặng nề ở onPause(), bạn có thể cân nhắc gọi chúng ở onStop().
### **onStop()**
-> onStop() được gọi khi Activity không còn được nhìn thấy nữa, có thể một màn hình nào khác che lên hoàn toàn, có thể một ứng dụng nào đó vào foreground, hoặc người dùng nhấn nút Home để về màn hình chính.
Bạn có thể tận dụng onStop() để lưu trữ dữ liệu ứng dụng. Hoặc để giải phóng các tài nguyên đang dùng. Ngưng các API còn đang gọi dang dở.
Tuy nhiên khi onStop() được gọi không phải là lúc chúng ta cũng nói lời tạm biệt Activity. Như mình đã nói, người dùng hoàn toàn có thể quay lại sử dụng Activity sau đó mà không cần phải khởi động lại Activity, khi này thì phương thức onRestart() và onStart() được gọi kế tiếp nhau.
### **onDestroy()**
-> Bạn có thể tận dụng callback này để giải phóng các tài nguyên hệ thống mà ở onStop() bạn chưa gọi đến.
Vòng đời của một Activity kết thúc ở đây.
# 3. findViewById
- Khi lập trình Android, để tương tác với các View/Control trong giao diện chúng ta thường thông qua thuộc tính Id của các View/Control để truy suất thay đổi dữ liệu. 
- Vì Android chia màn hình (Activity) thành hai phần: Phần thiết giao diện, phần xử lý nghiệp vụ. Do đó để truy suất được tới các View trong phần giao diện Android cung cấp hàm `findViewById`
- Ví dụ minh họa:
![](https://imgur.com/JtT814D.png)
- Ta chú ý mỗi lần đặt Id cho bất kỳ một View nào đó thì Id này sẽ tự động được phát sinh ra trong lớp R của Android. Vì vậy khi truy suất tới View ta dùng `R.id.idView`.
# 4. View Binding
- `View Binding` hoạt động với XML hiện tại của bạn và sẽ tạo một đối tượng binding cho mỗi layout trong một module
- Để sử dụng `View Binding` thêm 1 hàm :
``` cpp           
    buildFeatures {
        viewBinding true
    }
``` 
vào trong phương thức `android` thuộc `build.gradle(Module:app)`. Sau đó nhớ chọn `Sync Now`.
- `View Binding` tạo ra một class Java thay thế nhu cầu về `findViewById` trong code của bạn. Nó sẽ tạo ra một đối tượng liên kết cho mọi bố cục XML trong module của bạn trong khi ánh xạ các tên để `activity_main.xml` ánh xạ sang `ActivityMainBinding.java`. 
- Khi chỉnh sửa bố cục XML trong Android Studio, việc tạo code sẽ được tối ưu hóa để chỉ cập nhật đối tượng liên kết liên quan đến tệp XML đó và nó sẽ làm như vậy trong bộ nhớ để giúp mọi việc nhanh chóng. Điều này có nghĩa là các thay đổi đối tượng ràng buộc có sẵn ngay lập tức trong trình chỉnh sửa và bạn không cần phải rebuild lại project.
- Sử dụng:
    - Khai báo một đối tượng trùng tên với file xml
    - Khởi tạo và `setContentView`
    - ```cpp
        private ActivityMainBinding activityMainBinding;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            activityMainBinding = ActivityMainBinding.inflate(getLayoutInflater());
            setContentView(activityMainBinding.getRoot());
        }
    ``` ```
# 5. Intent
## 5.1. Định nghĩa
- `Intent` là một khái niệm khá trừu tượng về công việc, chức năng có thể được thực hiện bởi ứng dụng của bạn. Intent có thể được dùng để kết nối các thành phần trong ứng dụng Android. Trong quá trình kết nối, nó cũng có thể yêu cầu thành phần đó thực hiện một tác vụ được định trước.
- Các thành phần cơ bản của một Intent:
    - **Actions**: Là những thứ mà Intent cần thực thi, chẳng hạn như quay số điện thoại, mở URL hoặc chỉnh sửa dữ liệu. Một action đơn giản là một String mô tả cho tác vụ cần thực hiện. Ví dụ: ACTION_VIEW, ACTION_EDIT, ACTION_MAIN…
    - **Data**: Đây chính là dữ liệu để intent hoạt động. Nó được biểu diễn dưới dạng Uniform Resource Identifier(Uri) – một kiểu định danh cho một tài nguyên cụ thể. Kiểu của Data yêu cầu (nếu có) tùy thuộc vào action. Ví dụ: Bạn sẽ không muốn tạo một dial number Intent mà lại lấy số điện thoại từ một hình ảnh đúng không?
- Action:
    - `ACTION_VIEW`: như tên gọi của nó activity gửi intent với một action là ACTION_VIEW có nghĩa activity tương thích với intent này đang có thông tin để hiển thị cho người dùng như xem ảnh trong ứng dụng gallery hay xem địa chỉ trong google map (hay hiểu đơn giản Activity A đang muốn xem thông tin đc hiển thị ở Activity B)
    - `ACTION_SEND`: Còn được gọi là Intent chia sẻ. sử dụng action này trong trường hợp bạn có một số dữ liệu mà người dùng có thể chia sẻ thông qua một ứng dụng khác (chẳng hạn như facebook, email, các ứng dụng mạng xã hội)
    - Ngoài các action có sẵn như trên bạn có thể chỉ định action cho một intent với setAction hoặc hàm tạo Intent
- Data:
    - Sử dụng một đối tượng Uri tham chiếu tới dữ liệu sẽ đc thực hiện một hành động nào đó. Loại dữ liệu cung cấp thường được quyết định bởi action của intent. Ví dụ nếu action là ACTION_EDIT => Uri tham chiếu tới data đang cần edit
    - Khi tạo một intent không tường minh điều quan trọng là chỉ định kiểu dữ liệu, điều này sẽ giúp hệ thống android có thể tìm thấy thành phần tốt nhất để nhận intent của bạn
    - để set data sử dụng method setData():
    - để set type sử dụng method setType() Example:
    - ``` cpp
        Intent sendIntent = new Intent(Intent.ACTION_VIEW);
        sendIntent.setData(Uri.parse(Constant.TYPE_MESSAGE));
        sendIntent.setType("text/plain");
        startActivity(sendIntent);
        ```
## 5.2. Các loại Intent
### **Explicit Intent (Intent tường minh)**
- `Intent tường minh` tức là khi tạo một đối tượng Intent, chúng ta chỉ định rõ và truyền trực tiếp tên thành phần đích vào intent. Ví dụ: như đoạn code bên dưới, intent được chỉ định rõ OtherActivity sẽ là thành phần nhận và xử lý intent này.
- ```cpp
    val intent = Intent(this, OtherActivity::class.java)
    startActivity(intent)
    ```
### **Implicit Intent (Intent không tường minh)**
- `Intent không tường minh` tức là thay vì trong intent  Android được chỉ định sẵn một Activity nào đó thực hiện, thì sẽ chỉ truyền vào action và gửi cho Android. Android sẽ dựa vào action đó mà lọc những thành phần nào đã đăng kí action đó gọi ra.
- Vì vậy, Android có thể tự động kích hoạt thành phần từ cùng một ứng dụng hoặc một số ứng dụng khác để xử lý intent đó.
- Ví dụ, chúng ta cần phải hiển thị một vị trí lên bản đồ. Thay vì chúng ta phải mã hóa và viết hẳn module bản đồ để hiển thị thì có thể gửi vị trí đó vào intent, rồi Android sẽ tự tìm xem có ứng dụng nào phù hợp( như Google Map chẳng hạn) để hiển thị nó.
- Đây là một đoạn code minh họa cho intent không tường minh( sử dụng ACTION_VIEWđể gọi ứng dụng nào có thể hiển thị được link)

- ```cpp
    class ImplicitIntentActivity : AppCompatActivity() {
    
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(R.layout.activity_implicit_intent)
        }
    
        fun showWebPage(view: View) {
            val intent = Intent(Intent.ACTION_VIEW,
                    Uri.parse("http://www.ebookfrenzy.com"))
    
            startActivity(intent)
        }
    }
    ```

***NOTE:*** `Thông thường, chúng ta dùng các intent tường minh để kích hoạt các thành phần trong ứng dụng, còn intent không tường minh để chạy các thành phần của ứng dụng bên thứ 3.`
## 5.3. Truyền dữ liệu giữa các Activity bằng Intent
- Để truyền dữ liệu sang cho activity mới chúng ta sử dụng các cặp key-value trong hàm `putExtra`, `putStringArrayListExtra`.
- `putExtra` chỉ truyền được dữ liệu kiểu cơ bản: Int, Float, Char, Double, Boolean, String
- Ví dụ:
``` cpp
val intent = Intent(this, OtherActivity::class.java)
intent.putExtra("keyString", "Androidly String data")
```