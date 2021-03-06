---
layout: post
title: Responsive Layout and Fill Mode on Video.js
---

> Video.js release v7.3.0 brings a long wanted feature: Responsive Layout. In addition, Fill Mode has been promoted to a first-class feature

Phát hành Video.js v7.3.0 mang đến một tính năng mong muốn từ lâu: Giao diện đáp ứng. Ngoài ra, Chế độ điền đã được thăng cấp lên tính năng hạng nhất

### Responsive Mode

Chế độ Responsive sẽ giúp người chơi điều chỉnh các thành phần UI theo kích thước của trình phát. Nó sử dụng sự kiện playerresize đã được thêm vào v6.7.0 của Video.js, cho phép chúng tôi biết khi nào trình phát thay đổi kích thước.

Chế độ Responsive sẽ thiết lập và thay đổi các lớp điểm dừng nhất định như `vjs-layout-small` khi kích thước trình phát thay đổi. Đây có thể được cấu hình. Tùy thuộc vào lớp nào hiện đang có trên trình phát, thanh điều khiển và các thành phần UI khác có thể thích ứng.
Ví dụ: với `vjs-layout-small`, các điều khiển thời gian sẽ không hiển thị vì các công cụ thời gian trên thanh tiến trình có sẵn và nút chú thích quan trọng hơn. Ở kích thước lớn hơn, cả hai có thể được hiển thị mà không có vấn đề.

Bạn có thể tìm hiểu cách bật `Responsive Mode` và hơn thế nữa trong trang [tài liệu](https://docs.videojs.com/tutorial-layout.html#responsive-mode) của chúng tôi. Ngoài ra còn có một [example playground](https://github.com/videojs/video.js/blob/master/sandbox/responsive.html.example) trong thư mục sandbox trong repo.

Một người chơi trong chế độ 'responsive ' sẽ thêm và xóa các lớp dựa trên các breakpoints kích thước của nó. Các breakpoints, class và kích thước mặc định được nêu bên dưới:

| Name |  |  | Class |  |  | Min. Width | Max. Width |
| -- | -- | -- | -- | -- | -- | -- | -- |
| `tiny`   |  |  |  `vjs-layout-tiny`    |  |  | 0 | 210 |
| `xsmall` |  |  |  `vjs-layout-x-small` |  |  | 211 | 320 |
| `small`  |  |  |  `vjs-layout-small`   |  |  | 321 | 425 |
| `medium` |  |  |  `vjs-layout-medium`  |  |  | 426 | 768 |
| `large`  |  |  |  `vjs-layout-large`   |  |  | 769 | 1440 |
| `xlarge` |  |  |  `vjs-layout-x-large` |  |  | 1441 | 2560 |
| `huge`   |  |  |  `vjs-layout-huge`    |  |  | 2561 | Infinity |

Bạn có thể bật chế độ `responsive` bằng cách chuyển tùy chọn `responsive` hoặc bằng cách gọi `player.responsive(true)`.

{% highlight js %}
var player = videojs('vid1', {
  responsive: true
});
{% endhighlight %}

{% highlight js %}
var player = videojs('vid2');

player.responsive(true);
{% endhighlight %}

Chế độ `Responsive` độc lập với `fluid mode` hoặc `fill mode` - nó chỉ liên quan đến sự sắp xếp của UI trong trình phát, không phải với kích thước của trình phát. Tuy nhiên, thường hữu ích khi sử dụng 'Responsive mode' kết hợp với `fluid mode` hoặc `fill mode`!

### Fluid Mode
Video.js ở chế độ Fluid sẽ giữ cho trình phát có kích thước theo tỷ lệ khung hình cụ thể.

Theo mặc định, chế độ fluid sẽ sử dụng kích thước nội tại của video khi được tải nhưng bạn có thể thay đổi nó bằng các lớp hoặc với tùy chọn `aspectRatio`.

Bạn có thể kích hoạt fluid theo một số cách:
- Thêm `vjs-liquid`, `vjs-16-9` hoặc `vjs-4-3` làm class cho thành phần người chơi.
- Truyền tùy chọn `fluid` cho người chơi.
- Gọi `player.fluid(true)`.
- Truyền tùy chọn `aspectRatio` cho người chơi.
- Gọi `player.aspectRatio('16:9')`.

{% highlight js %}
var player = videojs('vid1', {
  fluid: true
});
{% endhighlight %}

{% highlight js %}
var player = videojs('vid2');

player.fluid(true);
{% endhighlight %}


##### Aspect Ratio - Tỷ lệ khung hình
Có ba class liên quan đến chế độ Fluid, `vjs-liquid`, `vjs-16-9` và `vjs-4-3`.

`vjs-liquid` bật chế độ Fluid chung sẽ đợi video tải để tính tỷ lệ khung hình của video.

Ngoài ra, vì tỷ lệ khung hình `16:9` và `4:3` rất phổ biến, chúng tôi đã cung cấp chúng dưới dạng các class theo mặc định để bạn sử dụng nếu bạn biết rằng video của mình là 16:9 hoặc 4:3.

Bạn có thể chỉ định tỷ lệ khung hình để chúng tôi sử dụng nếu bạn không muốn sử dụng các giá trị nội tại từ thành phần video hoặc nếu bạn có một tỷ lệ cụ thể trong tâm trí. Nó hoạt động như một cuộc gọi phương thức hoặc một tùy chọn cho người chơi.

Tùy chọn này ở dạng hai số nguyên được phân tách bằng dấu hai chấm như `21:9`, `16:9` hoặc `4:3`.

{% highlight js %}
// make a vertical video
var player = videojs('vid1', {
  aspectRatio: '9:16'
});
{% endhighlight %}

{% highlight js %}
var player = videojs('vid2');

// make a square video
player.aspectRatio('1:1');
{% endhighlight %}


### Fill Mode
[Fill Mode](https://docs.videojs.com/tutorial-layout.html#fill-mode) cho phép trình phát Video.js thay đổi kích thước linh hoạt, nhưng vẫn nằm trong giới hạn của vùng chứa chính nó. Điều này tương tự với [Fluid Mode](https://docs.videojs.com/tutorial-layout.html#fluid-mode), nhưng đôi khi, hộp chứa của bạn đã được đặt đúng kích cỡ.

Bạn có thể chuyển trong tùy chọn `fill` vào trình phát hoặc gọi `player.fill(true)`. Điều này sẽ kích hoạt chế độ fill.
{% highlight js %}
var player = videojs('vid1', {
  fill: true
});
{% endhighlight %}

{% highlight js %}
var player = videojs('vid2');

player.fill(true);
{% endhighlight %}

Kích hoạt chế độ fluid sẽ vô hiệu hóa chế độ fill. Nếu cả hai được kích hoạt, chế độ chất fluid được ưu tiên.

Fill Mode không phải là một chế độ hoàn toàn mới, lớp `vjs-fill` đã có sẵn trong Video.js khá lâu. Điều này cuối cùng làm cho nó trở thành một tính năng hạng nhất đi cùng với Chế độ Fluid.


-----
Reference
- [Tutorial: layout Video.js Documentation](https://docs.videojs.com/tutorial-layout.html)
- [Video.js 7.3: Responsive Layout, Fill Mode, createLogger](https://blog.videojs.com/video-js-7-3-responsive-layout-fill-mode-createlogger/)
