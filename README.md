# [Structuring your Sass Projects](https://itnext.io/structuring-your-sass-projects-c8d41fa55ed4)

## [Cấu trúc trong project Sass của bạn](https://itnext.io/structuring-your-sass-projects-c8d41fa55ed4)

![](https://cdn-images-1.medium.com/max/1600/1*MCiNLBzUI-LWK_PhVwq0xA.png)

Hãy xem lại cách mà chúng ta cấu trúc các project Sass của mình. Khi các dự án phát triển và mở rộng, nhu cầu cấu trúc modul hoá các thư mục và các file của chúng tôi tăng lên đáng kể. Vì vậy, để giữ được tổ chức đối với các file và thư mục là rất quan trọng. Chúng tôi cũng có thêm lợi ích từ việc tạo các thành phần có thể tái sử dụng trên nhiều dự án khác nhau. Không có bất kì một cấu trúc nào coi là chính xác hoàn toàn - nó phụ thuộc vào bản thân bạn.

Bài viết này là bài sau của [Bắt đầu với Sass](https://medium.com/@timothyrobards/starting-with-sass-116f4ecb682d), chúng tôi đã được học về các tính năng giúp Sass trở thành 1 công cụ đắc lực, cũng như việc làm sao để cài đặt môi trường phát triển Sass phía local.

**Làm sao để chúng ta cấu trúc được các dự án Sass?**

Chúng tôi thực hiện việc này bằng cách sử dụng *Partials* chia các stylesheet thành nhiều file khác nhau. Các file riêng biệt sẽ đại diện cho các thành phần khác nhau. Sau đó *import* các phần của chúng vào một stylesheet chính bằng cách sử dụng chỉ thị `@import`, thường là file `main.scss`. Ví dụ:

```scss
// File: main.scss
@import 'layout/header';
```

Chúng tôi cũng tạo thêm thư mục layout cho các file layout cụ thể của mình, ví dụ như là:

```scss
// File: _header.scss
// This file contains all styles related to the header of the site/application.
/* STYLES GO HERE */
```

*Chú ý:* tên của file partial luôn bắt đầu với dấu gạch dưới `_`.

Bây giờ hãy xem làm sao để cấu trúc lại project của bạn.

### Cấu trúc đơn giản

Nếu bạn đang sử dụng Sass cho một dự án nhỏ, ví dụ như một single web page. Một cấu trúc thu gọn có thể làm như sau:

```
_base.scss
_layout.scss
_components.scss
main.scss
```

Đây là 3 thành phần kết nối tới file `main.scss` của chúng ta.

**Base:** trong file này là toàn bộ các thành phần reset, variable, mixin và các class untility khác.

**Layout:** chứa các CSS xử lý layout, như là container và các hệ thống grid.

**Components:** mọi thứ có tính sử dụng lại như các button, navbar, card,...

**Main:** nó chỉ chứa các chỉ thị import đối với các file trên.

Nếu có bất kì file nào phát triển quá lộn xộn hoặc không có tổ chức, thì đây là lúc chúng ta mở rộng cấu trúc của mình. Ví dụ như, xem xét việc thêm một thư mục cho các thành phần của bạn, và chia nó thành các file riêng như `_button.scss` và `_carousel.scss`.

Tuy nhiên, khi chúng ta làm việc với dự án lớn, chúng ta cần một cấu trúc chặt chẽ hơn, mà chúng ta sẽ xem xét trong phần tiếp theo.

### The 7–1 Pattern - Mô hình 7-1

Một kiến trúc được biết đến như `7-1 pattern` ( 7 thư mục, 1 file), là một cấu trúc được áp dụng rộng rãi làm cơ sở cho các dự án lớn. Các thành phần của bạn được tổ chức trong 7 thư mục và chỉ có 1 file  đặt ở level root (thường có tên là `main.scss`) để xử lý các import - và là file được biên dịch thành CSS. 

Đây là một ví dụ về cấu trúc thư mục 7-1. Tôi đã thêm một vài file ví dụ và đặt chúng vào mỗi folder:

```
sass/
|
|– abstracts/ (or utilities/)
|   |– _variables.scss    // Sass Variables
|   |– _functions.scss    // Sass Functions
|   |– _mixins.scss       // Sass Mixins
|
|– base/
|   |– _reset.scss        // Reset/normalize
|   |– _typography.scss   // Typography rules
|
|– components/ (or modules/)
|   |– _buttons.scss      // Buttons
|   |– _carousel.scss     // Carousel
|   |– _slider.scss       // Slider
|
|– layout/
|   |– _navigation.scss   // Navigation
|   |– _grid.scss         // Grid system
|   |– _header.scss       // Header
|   |– _footer.scss       // Footer
|   |– _sidebar.scss      // Sidebar
|   |– _forms.scss        // Forms
|
|– pages/
|   |– _home.scss         // Home specific styles
|   |– _about.scss        // About specific styles
|   |– _contact.scss      // Contact specific styles
|
|– themes/
|   |– _theme.scss        // Default theme
|   |– _admin.scss        // Admin theme
|
|– vendors/
|   |– _bootstrap.scss    // Bootstrap
|   |– _jquery-ui.scss    // jQuery UI
|
`– main.scss              // Main Sass file
```

**Abstracts (or utilities):** chứa các công cụ Sass, các file helper, variables, function, mixin và các file config. Các file này chỉ có tính hỗ trợ, không tạo ra bất kì CSS nào khi biên dịch. 

**Base:** giữ các đoạn code sẵn cho project. Bao gồm cả các style chuẩn như reset và các rule typographic, mà chúng thường được dùng trong project của bạn.

**Component (hoặc Modules):** giữ các style như button, carousels, sliders và các thành phần tương tự trên trang (như widgets). Project của bạn sẽ chứa rất nhiều các file thành phần như này - vì toàn bộ trang web/ứng dụng bao gồm rất nhiều các module nhỏ.

**Layout:** chứa tất cả các style liên quan tới layout của project. Như là style của header, footer, navigation và hệ thống grid.

**Pages:** mọi style cụ thể cho các trang riêng sẽ được đặt ở đây. Ví dụ như nó không phổ biến đối với trang chủ của bạn mà chỉ được yêu cầu các style cụ thể của trang và không có trang nào khác nhận được.

**Themes:** cái này thường không được sử dụng trong nhiều project. nó chứa các file tạo theme cụ thể của dự án. Ví dụ như các phần cụ thể của trang web của bạn chứa các bảng màu để thay thế.

**Vendors:** chứa các phần code của bên thứ 3 từ các thư viện hoặc framework bên ngoài. ví dụ như Normalize, Bootstrap, jQueryUI,… Tuy nhiên nó từ không cần thiết trong việc phải ghi đè code trong vendor.. Nếu điều này là bắt buộc, giải pháp tốt nhất là tạo thêm 1 folder mới gọi là `vendor-extensions` / và sau đó đặt tên cho mọi file được ghi đè trong vendor. File `vendors-extensions/_bootstrap.scss nên chứa mọi ghi đè Bootstrap của bạn - khi tự chỉnh sửa các file vendor, nó thường không phải là ý tưởng tốt.

**Main.scss:** Đây là file chỉ chứa các import của bạn. Ví dụ...

```scss
@import 'abstracts/variables';
@import 'abstracts/functions';
@import 'abstracts/mixins';

@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/slider';

@import 'pages/home';
@import 'pages/about';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';
```

*Chú ý:* Không cần thiết thêm dấu `_` hoặc phần mở rộng  `.scss` của file khi import.

### Bắt đầu và chạy với 7-1 pattern

Bản chính thức đã có trên [github](https://github.com/HugoGiraudel/sass-boilerplate). Bạn có thể tải về hoặc clone nó bằng lệnh:

```
git clone https://github.com/HugoGiraudel/sass-boilerplate.git
```

### Tóm lại

Và điều đó. Bạn đã học làm sao để cấu trúc lại các project Sass của bạn. Điều cần lưu ý ở đây là không có bất kì quy tắc nào rõ ràng. Bạn nên cấu trúc dự án của mình theo cách có nghĩa nhất với bạn (và với team của bạn)!. Điều này giúp bạn tìm kiếm nhanh hơn, dễ dành hơn và cô lập được style của mình - đó là cách để làm việc!

Hãy xem qua bài tiếp theo trong series:[Thiết lập luồng Build Sass](https://medium.com/@timothyrobards/setting-up-a-sass-build-process-aa9fd92fa585). Khi chúng tôi sử dụng các script npm để thiết lập quy trình build một project sẽ thúc đẩy đáng kể đối với quy trình phát triển của chúng tôi…
