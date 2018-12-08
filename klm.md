
# Các mô đun tải thêm vào lõi Linux 

Source: http://www.tldp.org/HOWTO/html_single/Module-HOWTO/index.html

Lõi là một phần rất quan trọng của hệ điều hành Linux. Nhưng tinh thần của hệ điều hành nguồn mở là bạn can thiệp kiểu gì cũng được. Vì vậy bạn hoàn toàn có thể tự thêm code bạn viết vào lõi. Cách một là thêm tập tin chứa code vào thư mục nguồn của lõi và soạn lại lõi (*recompile*). Khi bạn tự thiết lập lõi cũng là khi bạn chọn những tập tin nào bạn thích để soạn thành lõi đó. 

Cách thứ hai là thêm code vào lõi Linux khi nó đang chạy. Tức là tải thêm một mô đun lõi cơ động. Những mô đun này có thể làm rất nhiều thứ, nhưng chủ yếu là ba thứ: người lái thiết bị, người lái tập tin hệ thống, hoặc cuộc gọi hệ thống. Lõi cô lập và quản lý riêng các chức năng cực kỳ tốt cho nên chúng không cần phải được nối dây rợ tỉ mỉ vào lõi. Ta tải vào rồi tải ra dễ dàng.

Mô đun là một khái niệm chung chung, bất cứ thành phần nào của cái gì mà đủ riêng biệt để đứng độc lập đều có thể gọi là mô đun. Mô đun tải thêm vào lõi cũng vậy. Cũng là một tập tin code dùng để phục vụ một mục đích nào đó giúp tăng chức năng của lõi. Các mô đun này là một phần của lõi. Còn phần code căn bản: *lõi* của lõi (phần ảnh mà bạn *boot*) hay nói cách khác, phần lõi mà không phải do bạn tải thêm vào, gọi là phần căn lõi. Các mô đun phụ tải thêm vào sẽ giao tiếp với căn lõi, nhưng những mô đun phụ này vẫn được gọi và tính là lõi. Trong một số hệ điều hành khác, họ gọi mô đun phụ là lõi mở rộng (như kiểu Hà Nội 2).

Về từ Linux, Linux có thể dùng để chỉ 2 thứ riêng biệt:
* Phần lõi và các vật phẩm liên quan mà được Linus Torvald đóng gói và phổ biến 
* Một tập hợp của cả hệ điều hành mà theo truyền thống được xây bao quanh lõi Linux. Hệ điều hành bao gồm lõi và to hơn lõi nhiều, và các chương trình khác lõi được viết bởi GNU cho nên ta có thể gọi là GNU/Linux. 

Trong bài này, khi nói đến Linux, ta nói đến lõi Linux ở ý một. Về mặt kỹ thuật, lõi Linux là bộ code được đóng gói và phổ biến bởi Linus Torvald, cho nên nếu bạn tự tải thêm một người vận hành thiết bị (cung cấp cho bạn bởi người cung cấp thiết bị này) thì lõi đó (với tính năng thêm) đã trở thành một phiên bản khác đi một tị của lõi Linux. Nhưng bạn có thể hiểu là, thường thì người ta gọi Linux một cách chung chung, không cần kỹ tính đến thế, rất nhiều các phiên bản Linux được dùng và phổ biến rộng rãi, đều được gọi chung là Linux. Trong bài này, ta sẽ nói đến lõi Linux theo định nghĩa chặt chẽ của nó, để cho dễ.

Ban đầu ta chưa có khái niệm về mô đun tải thêm. Những thứ mà ngày nay ta dùng như mô đun tải thêm đều được xây sẵn vào căn lõi trước đó. Tất nhiên như thế không được thoải mái lắm. Khoảng 1995 (Linux phiên bản 1.2) thì người ta bắt đầu làm lõi một cách thoải mái hơn, có khái niệm mô đun tải thêm. Ta có thể thấy rằng, việc coi các thiết bị và người vận hành thiết bị như mô đun riêng là tự nhiên của quá trình tiến hóa. Ban đầu, ta chỉ cần chỉnh sửa chút là mô đun sẽ thành mô đun tự tải thêm được. Tuy nhiên, phải làm riêng cho từng cái nên hơi khó. Từ khoảng năm 2000, hầu hết bất cứ cái gì mà về mặt logic có thể coi như mô đun tự tải thêm đều có sự lựa chọn để trở thành mô đun tải thêm.

Tinh thần là bạn luôn có thể lựa chọn giữa chạy mô đun như một mô đun tải thêm hoặc xây thẳng nó vào căn lõi. Sử dụng chúng như mô đun tải thêm có rất nhiều lợi thế và bạn nên chọn sự lựa chọn này khi có thể.

Một lợi thế là bạn không phải xây lại lõi thường xuyên và vì thế giảm lỗi. Một khi bạn xây được lõi chạy được rồi thì tốt nhất là đừng động vào nữa. Một lợi thế khác là bạn có thể chẩn đoán các vấn đề hệ thống dễ dàng hơn. Nếu người vận hành thiết bị bị lỗi, mà chương trình này lại được xây thẳng vào lõi thì có khi là cả hệ thống của bạn không *boot* lên được. Khi đó rất khó để đoán ra phần nào có lỗi. Nếu cùng một người vận hành thiết bị đó, nhưng sau khi lõi chạy hắn mới được tải thêm vào như một mô đun tải thêm, thì ta dễ dàng hiểu được là người vận hành thiết bị đó có vấn đề và không cần tải chương trình đó cho đến khi bạn sửa xong. 

Khi tải các mô đun riêng, bạn tiết kiệm bộ nhớ, bởi vì bạn chỉ tải khi nào bạn cần dùng mà thôi. Trong khi đó, tất cả các phần của căn lõi sẽ được tải và chạy liên tục trong bộ nhớ thật, không phải bộ nhớ ảo.

Các mô đun riêng giúp bạn dễ bảo quản và tìm lỗi hơn. Nếu bạn xây người vận hành tập tin hệ thống thẳng vào lõi, bạn sẽ phải *boot* lại toàn bộ hệ thống, thế nhưng nếu hắn chỉ là mô đun tải thêm, bạn chỉ cần chạy vài dòng lệnh. Bạn cũng có thể thử những thông số kỹ thuật khác nhau hoặc thay đổi code liên tục và thử đi thử lại mà không cần đợi *boot*.

Các mô đun riêng cũng không chậm hơn mô đun ở trong căn lõi. Về mặt kỹ thuật, gọi chúng lên đều là mở thêm một nhánh tới địa chỉ bộ nhớ mà chúng đang nằm đợi.

Thi thoảng, bạn sẽ cần phải xây trực tiếp một tính năng vào căn lõi thay vì làm chúng riêng rẽ thành mô đun tải thêm. Hiển nhiên là bất cứ cái gì bắt buộc phải có khiến cho hệ thống chạy được tới điểm hắn có khả năng tự tải thêm mô đun cần phải được xây thẳng vào căn lõi. Ví dụ, chương trình người vận hành ổ đĩa dùng để chạy ổ đĩa nào mà chứa tập tin hệ thống cần phải được xây thẳng vào căn lõi.

Bạn có thể thấy là các mô đun lõi này giống các chương trình người dùng, nhưng không phải. Bọn chúng là một phần của lõi, chúng có quyền chạy cao và dễ dàng làm sập hệ thống.

##

Các mô đun tải thêm được dùng cho 6 mục đích sau:

* Người vận hành thiết bị. Một chương trình người vận hành thiết bị là một chương trình được thiết kế cho một mảnh phần cứng nhất định. Lõi sẽ dùng chương trình đó để giao tiếp với phần cứng đó mà không cần biết cụ thể phần cứng đó làm việc như thé nào. Ví dụ, có người vận hành riêng cho ổ đĩa ATA. Có một người khác cho thẻ ethernet NE2000 đa dụng. Để sử dụng bất cứ thiết bị nào, lõi phải có một người vận hành thiết bị riêng cho thiết bị đó.

* Người vận hành tập tin hệ thống. Người vận hành tập tin hệ thống sẽ phiên dịch nội dung của một tập tin hệ thống (tức là nội dung nằm trên ổ đĩa) như tập tin và thư mục. Có rất nhiều cách khác nhau để lưu tập tin và thư mục trên ổ đĩa, trên máy phục vụ ở đâu đó trên mạng vv. Mỗi một cách lại cần một người vận hành tập tin hệ thống khác nhau. Ví dụ, có một người vận hành tập tin hệ thống cho kiểu tập tin hệ thống ext2 khá phổ biến trên ổ đĩa Linux (ở thời điểm viết này có thể là chuẩn cao hơn rồi). Có một người vận hành cho tập tin hệ thống MS DOS và NFS nữa.

* Cuộc gọi hệ thống. Các chương trình người dùng gọi hệ thống để sử dụng dịch vụ do lõi cung cấp. Ví dụ, chương trình biên tập văn bản gọi lõi để nhờ đọc hộ tập tin đang nằm đâu đó trên đĩa cứng, hoặc để tạo chương trình mới, hay để tắt máy đi. Hầu hết các cuộc gọi hệ thống đều là một phần của hệ thống và thành chuẩn rồi nên luôn được xây vào căn lõi (không có lựa chọn để làm thành mô đun riêng). Nhưng bạn có thể nghĩ ra cuộc gọi mới và cài đặt như là mô đun riêng. Hoặc bạn không thích cách mà Linux đang làm và muốn viết đè lên một cuộc gọi hệ thống bằng code của riêng bạn.

* Người vận hành mạng. Người vận hành mạng là chương trình thông dịch chuyên về mạng. Hắn ăn và nhả ra các dòng dữ liệu ở các lớp khác nhau của các chức năng mạng của lõi. Ví dụ, nếu bạn muốn kết nối IPX trong mạng của bạn, bạn dùng người vận hành 
IPX

* TTY. Đây là phần xây thêm của người vận hành hệ thống cho các thiết bị cổng giao tiếp phần cứng. 

* Người thông dịch các đoạn mã chạy được (*executable*). Người thông dịch sẽ tải và chạy các đoạn mã này. Linux chạy được các đoạn mã có cấu trúc (*format*) khác nhau, với những người thông dịch khác nhau.

##

Một mô đun tải thêm sống trong một tập tin vật thể ELF (đuôi .o nghĩa là *object*, vật thể). Bạn cho đám tập tin này ở chung một thư mục nhất định (gần ảnh của căn lõi là lựa chọn tốt). Khi bạn dùng *insmod* để chèn mô đun vào lõi, bạn đưa cho  hắn tên của tập tin vật thể đó. 

Với những mô đun riêng mà đi kèm trong gói Linux, bạn xây chúng trong quá trình xây lõi để tạo ra ảnh căn lõi. Bạn có thể xem thêm trong tập tin README ở cây nguồn Linux. Nói ngắn, sau khi bạn tạo ra ảnh căn lõi với lệnh như ```make zImage```, bạn sẽ tạo các mô đun riêng với lệnh ```make modules```. Lệnh này sẽ tạo ra một loạt tập tin vật thể (*.o) trong cây nguồn Linux. Những mô đun này sẵn sàng đợi tải, nhưng bạn nên cài chúng vào các thư mục phù hợp. Lệnh ```make modules_install``` sẽ sao chép chúng vào các vị trí phù hợp.

Một phần của việc hiệu chỉnh lõi Linux (ở thời điểm xây) là chọn phần lõi nào để xây thẳng vào căn lõi và phần nào thì xây thành mô đun riêng. Với những phần tùy chọn thêm vào cho lõi, bạn sẽ được hỏi, liệu bạn muốn xây thẳng vào lõi hay xây thành mô đun riêng, hay bỏ qua không làm gì cả. Như đã nói ở trên, bạn xây thẳng vào lõi ít nhất có thể, và chỉ bỏ qua những phần bạn chắc chắn là không bao giờ cần.

Các mô đun mà không phải mô đun được đóng gói sẵn trong lõi Linux có qusa trình xây riêng nhưng cuối cùng vẫn cần tạo ra tập tin vật thể ELF. Bạn cũng không cần xây lại ảnh căn lõi và các mô đun cùng lúc. Bạn có thể xây lại căn lõi không và dùng lại các mô đun đã xây trước đó, tuy nhiên xây lại cùng lúc là ý kiến hay.

### 

Các chương trình giúp bạn tải vào tải ra và các hoạt động khác nằm trong gói modutils (*module utils*):

* insmod: chèn mô đun vào lõi (*insert module*)
* rmmod: bỏ mô đun ra khỏi lõi (*remove module*)
* depmod: xem xét các mối liên hệ giữa các mô đun (*dependent modules*)
* kerneld: *deamon* của lõi (cu-li lõi :) (*kernel deamon*)
* ksyms: hiển thị biểu tượng mà lõi xuất ra cho mô đun mới dùng 
* lsmod: hiển thị các mô đun đang được tải (*list modules*)
* modinfo: hiển thị nội dung của đoạn ```.modinfo``` trong tập tin vật thể của một mô đun (chứa đựng thông tin về mô đun) (*module info*)
* modprobe: chèn hoặc gỡ một mô đun hoặc một bộ các mô đun một cách thông minh. Ví dụ, nếu bạn phải tải A trước khi tải B, ```modprobe``` sẽ tự động tải A khi bạn bảo nó tải B đi (*modul probe*)

Khi ta thay đổi lõi, thường ta phải thay đổi modutils vì vậy cần lấy bản modutils mới khi cập nhật lõi. modutils lúc nào cũng chạy được với các bản lõi cũ hơn (*backward compatible*) vì vậy không phải lo ta có trong tay bản modutils mới quá.

### Chèn và gỡ mô đun 

Chương trình căn bản để chèn và gỡ mô đun là **insmod** và **rmmod**. Chèn mô đun nghe rất dễ: gõ vào (với tư cách người dùng chủ) dòng lệnh kiểu như ```insmod serial.o``` (gọi người vận hành cổng serial UARTs). Thế nhưng, rất dễ phát điên, bởi vì dòng lệnh này thường trả về một tấn lỗi, đơn cử là phiên bản mô đun và lõi không hợp nhau.

