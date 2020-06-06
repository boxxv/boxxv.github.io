---
layout: post
title: Upgrading npm dependencies
subtitle: Cập nhật các thư viện phụ thuộc trong NPM
---

Làm thế nào chúng ta có thể nâng cấp một cách an toàn các phụ thuộc npm trong dự án của chúng ta? Các ký tự ^ và ~ có nghĩa là gì trước các phiên bản gói phụ thuộc? Làm thế nào chúng ta có thể nâng cấp phiên bản chính trên một phụ thuộc npm trong dự án của chúng ta? Chúng ta sẽ tìm ra trong bài viết này.

#### Version parts
Phiên bản gói npm theo quy tắc đánh version cho software gọi là Semantic Versioning. Vì vậy, một phiên bản gói có 3 phần - Major.Minor.Patch
- Major: tăng khi bạn thực hiện các thay đổi dẫn đến KHÔNG tương thích ngược.
- Minor: tăng khi bạn thêm tính năng và vẫn đảm bảo tương thích ngược (backwards-compatible).
- Patch: tăng khi bạn thực hiện fix lỗi xử lý bên trong và vẫn đảm bảo tương thích ngược (backwards-compatible)

#### ^ Và ~ có nghĩa là gì?

Một phiên bản thường có một ^ ở phía trước của nó (ví dụ ^ 16.8.6). Điều này có nghĩa là phiên bản nhỏ mới nhất có thể được cài đặt an toàn. Vì vậy, trong ví dụ này, ^ 16.12.1 có thể được cài đặt an toàn nếu đây là phiên bản mới nhất trong 16.x.

Đôi khi, một phiên bản có ~ ở phía trước của nó (ví dụ: ~ 16.8.6). Điều này có nghĩa là chỉ có phiên bản vá mới nhất có thể được cài đặt an toàn. Vì vậy, trong ví dụ này, ^ 16.8.12 có thể được cài đặt an toàn nếu đây là phiên bản mới nhất trong 16.8.x.


#### Vì vậy, `npm install` cài đặt phiên bản an toàn mới nhất của các phụ thuộc?

Có và không!

Nếu các gói đã được cài đặt vào thư mục `node_modules`, thì `npm install` sẽ không cập nhật bất kỳ gói nào.

Nếu các gói chưa được cài đặt và tồn tại trong tệp `pack-lock.json`, thì `npm install` sẽ cài đặt các phiên bản phụ thuộc chính xác được chỉ định trong gói-lock.json.

`npm install` sẽ cài đặt phiên bản an toàn mới nhất của các phụ thuộc nếu chúng không tồn tại trong thư mục `node_modules` và không có tệp `pack-lock.json`. Tuy nhiên, bạn có thể nghĩ rằng phiên bản an toàn mới nhất đã được cài đặt vì `package.json` không thay đổi, nhưng nếu bạn kiểm tra các gói trong thư mục `node_modules`, phiên bản an toàn mới nhất sẽ được cài đặt.


#### Vì vậy, làm thế nào để tôi cập nhật một cách an toàn tất cả các phụ thuộc?

Thứ nhất, các phụ thuộc đã hết hạn có thể được phát hiện bằng cách chạy lệnh sau:

{% highlight js %}
npm outdated
{% endhighlight %}






-----
### X. Resources
Dưới đây là một bản tóm tắt các tài nguyên bạn sẽ sử dụng trong khi làm việc thông qua sự khởi đầu nhanh chóng này. Các liên kết này cũng được cung cấp trong các bước dưới đây:
- [Upgrading npm dependencies](https://www.carlrippon.com/upgrading-npm-dependencies/)