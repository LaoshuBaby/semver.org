---
title: Ý nghĩa việc đánh số phiên bản 2.0.0
language: Tiếng Việt
---

Đánh số phiên bản 2.0.0
===

Tổng quan
---
Đưa ra một cấu trúc phiên bản MAJOR.MINOR.PATCH, gia tăng như thế này:
1. Số phiên bản MAJOR khi bạn có các thay đổi lớn về API
2. Số phiên bản MINOR khi bạn thêm chức năng tương thích ngược với phiên bản trước
3. Số phiên bản PATCH khi bạn làm một bản vá lỗi tương thích ngược với phiên bản trước

Bổ sung các nhãn cho tiền phát hành và xây dựng các siêu dữ liệu sẵn sàng như là một tiện ích mở rộng theo định dạng MAJOR.MINOR.PATCH

Giới thiệu
---

Trong thế giới của quản lý phần mềm, ở đó tồn tại một nơi được gọi là "địa ngục của sự phụ thuộc". Hệ thống của bạn ngày càng lớn hơn và bạn càng tích hợp nhiều gói vào trong phần mềm của mình hơn, Một ngày nào đó bạn sẽ tuyệt vọng tìm kiếm bản thân mình trong cái địa ngục này.

Trong các hệ thống có nhiều sự phụ thuộc, phát hành một phiên bản mới có thể nhanh chóng trở thành một cơn ác mộng. Nếu các thông số kỹ thuật phụ thuộc quá chặt chẽ với nhau, bạn đang ở trong sự nguy hiểm của khóa phiên bản (không có khả năng nâng cấp một gói mà không phải phát hành các phiên bản mới của mỗi gói phụ thuộc). Nếu các phụ thuộc được chỉ định rất lỏng lẻo, bạn chắc chắn sẽ ít mắc phải sự linh tinh phiên bản (giả định khả năng tương thích với nhiều phiên bản trong tương lai là hợp lý). Địa ngục của sự phụ thuộc là khi khóa phiên bản hoặc sự linh tinh của phiên bản ngăn cản bạn dễ dàng và an toàn chuyển tiếp dự án của mình.

Như là một giải pháp cho vấn đề này, tôi đề xuất một cách đơn giản để thiết lập các quy tắc và yêu cầu để làm thế nào gán và tăng dần các số phiên bản. Những quy tắc này là nền nhưng nó thực sự không cần thiết giới hạn đối với các thực tiễn phổ biến rộng rãi đã có từ trước được sử dụng trong cả phần mềm nguồn đóng và phần mềm mã nguồn mở. Để hệ thống này hoạt động, điều bạn cần làm đầu tiên là công bố một API công khai. Điều này có thể bao gồm các tài liệu hoặc được thực thi bởi mã của chính nó. Quan trọng là API phải rõ ràng và chính xác. Một khi bạn xác định API công khai của mình, bạn giao tiếp các sự thay đổi đến nó với các gia số cụ thể của mình. Cân nhắc về định dạng của phiên bản X.Y.Z (Major.Minor.Patch). Những bản sửa lỗi không ảnh hưởng đến đánh số tăng API phiên bản vá lỗi, bổ sung/thay đổi API tương thích ngược làm tăng phiên bản phụ và thay đổi API không tương thích ngược làm tăng phiên bản chính.

Tôi gọi hệ thống này là "đánh số phiên bản". Theo sơ đồ này, số phiên bản và cách chúng truyền đạt ý nghĩa các thay đổi từ phiên bản này qua phiên bản tiếp theo.   

Đặc điểm kỹ thuật của đánh số phiên bản (SemVer)
---
Các từ khóa “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, và “OPTIONAL” trong tài liệu này được giải thích như là một mô tả trong [RFC 2119](https://tools.ietf.org/html/rfc2119).

1. Phần mềm sử dụng đánh số phiên bản PHẢI tuyên bố một công khai API. API này cần công khai trong mã nguồn của nó hoặc nghiêm chỉnh tồn tại trong tài liệu. Tuy nhiên, nó phải chính xác và toàn diện.

2. Một chữ số phiên bản bình thường PHẢI lấy từ mẫu X.Y.Z. X, Y và Z là một số nguyên không âm, và không chứa số 0 ở chữ cái đầu tiên. X là phiên bản chính, Y là phiên bản nhỏ và Z là phiên bản vá lỗi. Mỗi yếu tố cần PHẢI là một số tăng dần. Cho ví dụ: 1.9.0 -> 1.10.0 -> 1.11.0.

3. Mỗi phiên bản cũ đã được phát hành, những nội dung của phiên bản cũ KHÔNG ĐƯỢC chỉnh sửa. Bất kỳ một sửa đổi cần PHẢI được phát hành vào một phiên bản mới.

4. Phiên bản chính zero (0.y.z) là dành cho nhà phát triển. Bất cứ thay đổi nào vào bất cứ thời gian nào. API công khai không nên được xem là ổn định.

5. Phiên bản 1.0.0 được xác định API công khai. Cái cách chọn trong mỗi con số tăng dần của phiên bản sau khi API công khai được phát hành là phụ thuộc vào chính API công khai và nó thay đổi như thế nào.

6. Bản vá lỗi Z (x.y.Z) PHẢI là tăng dần nếu chỉ là sửa cách lỗi tương thích ngược đã được giới thiệu. Một sửa lỗi được định nghĩa là một thay đổi nội bộ để sửa chửa một hành vi không chính xác.

7. Phiên bản nhỏ Y (x.Y.z) PHẢI là một số tăng dần nếu là mới, chức năng tương thích ngược được giới thiệu với API công khai. Nó PHẢI là số tăng dần nếu bất kỳ chức năng API công khai nào đã được đánh dấu là không còn dùng nữa. Nó CÓ THỂ tăng dần nếu chức năng mới hoặc cải tiến được giới thiệu trong mã riêng. Nó CÓ THỂ bao gồm thay đổi cấp độ bản vá. Phiên bản vá PHẢI được đặt lại về bằng 0 khi tăng phiên bản nhỏ.

8. Phiên bản chính X (X.y.z | X > 0) PHẢI là một số tăng dần nếu bất kỳ một thay đổi không tương thích ngược đưa vào API công khai. Nó CÓ THỂ bao gồm phiên bản phụ và thay đổi cấp độ bản vá. Bản vá và phiên bản phụ PHẢI được đặt lại về số 0 khi phiên bản chính tăng lên.

9. Phiên bản tiền phát hành CÓ THỂ được mô tả bằng cách nối thêm một dấu gạch nối vào một loạt số nhận dạng
được phân tách ngay sau phiên bản vá. Các định danh PHẢI bao gồm chữ số trong bảng mã ASCII và gạch nối \[0-9A-Za-z]. Các định danh KHÔNG ĐƯỢC để trống. Số định danh KHÔNG ĐƯỢC bao gồm các chữ số 0 đứng đầu. Các phiên bản tiền phát hành có một độ ưu tiên thấp hơn so với các phiên bản bình thường có liên quan. Một phiên bản tiền phát hành cho biết phiên bản không ổn định và có thể không đáp ứng các yêu cầu tương thích như dự định giống như là các phiên bản bình thường của nó. Ví dụ: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.

10. Xây dựng một siêu dữ liệu CÓ THỂ được thể hiện bằng cách nối thêm một dấu cộng và một loạt các tiền tố nhận dạng được phân tách bằng dấu chấm ngay sau phiên bản vá hoặc phiên bản tiền phát hành. Mỗi định danh PHẢI bao gồm chỉ các chữ số trong bảng mã ASCII và gạch nối \[0-9A-Za-z]. Mỗi định danh KHÔNG ĐƯỢC rỗng. Xây dựng một siêu dữ liệu NÊN bỏ qua khi quyết định ưu tiên phiên bản. Do đó hai phiên bản chỉ khác nhau trong việc xây dựng siêu dữ liệu, có cùng mức độ ưu tiên. Ví dụ: 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85.

11. Các ưu tiên đề cập đến cách các phiên bản được so sánh với nhau khi được đặt hàng. Ưu tiên PHẢI được tính bằng cách tách phiên bản thành các định danh chính, phụ, bản vá và tiền phát hành theo thứ tự đó (xây dựng siêu dữ liệu không được ưu tiên). Ưu tiên được xác định bởi sự khác biệt đầu tiên khi so sánh từ định danh này từ trái sang phải như sau: phiên bản chính, phiên bản phụ và bản vá nó luôn luôn được so sánh bằng số. Ví dụ: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1. Khi phiên bản chính, phiên bản phụ và bản vá bằng nhau, phiên bản tiền phát hành có mức độ ưu tiên thấp hơn phiên bản bình thường. Ví dụ: 1.0.0-alpha < 1.0.0. Ưu tiên của hai phiên bản tiền phát hành với cùng phiên bản chính, phiên bản phụ và bản vá PHẢI được xác định bằng cách so sánh từng số nhận dạng được phân tách bằng dấu chấm từ trái sang phải cho đến khi tìm thấy sự khác biệt như sau: các định danh chỉ bao gồm các chữ số được so sánh với chữ số và các định danh với chữ cái hoặc dấu gạch nối được so sánh theo từ vựng theo thứ tự sắp sếp trong bảng mã ASCII. Định danh dạng số luôn có độ ưu tiên thấp hơn hơn định danh không phải là dạng số. Một tập hợp các trường tiền phát hành lớn hơn có độ ưu tiên cao hơn các các trường tiền phát hành nhỏ hơn, nếu tất cả cách định danh bằng nhau. Ví dụ: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Tại sao nên sử dụng đánh số phiên bản?
---
Đây không phải là một ý tưởng mới hay mang tính cách mạng. Trong thực tế, bạn có thể làm một cái gì đó gần với điều này rồi. Vấn đề là "gần" cũng có nghĩa nó chưa đủ tốt. Không có tuân thủ một số kỹ thuật chính thức, số phiên bản về cơ bản là vô dụng để quản lý phụ thuộc. Bằng cách đặt tên và định nghĩa rõ ràng cho các ý tưởng trên, nó trở nên dễ dàng để truyền đạt ý định của bạn đến người dùng phần mềm của mình. Một khi những ý định này là rõ ràng, linh hoạt (nhưng không quá linh hoạt) thông số kỹ thuật phụ thuộc cuối cùng cũng có thể thực hiện.

Một ví dụ đơn giản chứng minh làm thế nào đánh số phiên bản có thể biến địa ngục phụ thuộc thành quá khứ. Xem xét một thư viện có tên là "Firetruck". Nó yêu cầu một gói về mặt ngữ nghĩa có tên "Ladder". Vào khoảng thời gian Firetruck được tạo, Ladder có phiên bản 3.1.0. Trước đó Firetruck sử dụng một số chức năng đã được giới thiệu lần đầu trong 3.1.0, bạn hoàn toàn có thể chỉ định một cách oan toàn phụ thuộc lớn hơn hoặc bằng 3.1.0 nhưng nhỏ hơn 4.0.0. Bây giờ, khi Ladder phiên bản 3.1.1. và 3.2.0 trở nên khả dụng, bạn cần phát hành chúng vào hệ thống quản lý gói của bạn và bạn biết rằng chúng sẽ tương thích với phần mềm phụ thuộc hiện có.

Như là một nhà phát triển có trách nhiệm bạn muốn, tất nhiên, muốn xác minh rằng bất kỳ gói nâng cấp đều hoạt động như đã quảng cáo. Thế giới thực là một nơi lộn xộn; không có gì chúng ta không thể làm nhưng hãy cảnh giác. Những gì bạn cần làm là hãy để đánh số phiên bản cung cấp cho bạn một cách lành mạnh để phát hành và nâng cấp các gói mà không cần phải cuộn các phiên bản mới của các gói phụ thuộc, tiết kiệm thời gian và rắc rối.

Nếu những điều này nghe có vẻ chờ đợi, tất cả những gì bạn cần để bắt đầu sử dụng đánh số phiên bản là tuyên bố bạn rằng bạn đang làm như vậy và tuân thủ theo các quy tắc. Liên kết trang web này từ README của bạn để những người khác có thể biết các quy tắc và có thể hưởng lợi từ chúng.

Câu hỏi thường gặp
---
###Làm thế nào tôi nên đối phó với các sửa đổi trong giai đoạn phát triển?
Điều đơn giản nhất để bắt đầu là bắt đầu phát hành bản dành cho nhà phát triển 0.1.0 và đánh số cho các phiên bản phụ cho mỗi lần phát hành tiếp theo.

###Làm thế nào để biết khi nào nên phát hành 1.0.0?
Nếu phần mềm của bạn đang được sử dụng trong sản xuất, nó có lẽ đã là 1.0.0. Nếu bạn có một API ổn định mà mỗi người dùng đã phụ thuộc vào, bạn nên là 1.0.0. Nếu bạn lo lắng rất nhiều về khả năng tương thích ngược, bạn có lẽ đã là 1.0.0.

###Điều này không ngăn cản sự phát triển nhanh chóng và nhanh lặp lại?
Phiên bản chính zero là tất cả về sự phát triển nhanh chóng. Nếu bạn thay đổi API mỗi ngày, bạn vẫn nên ở phiên bản 0.y.z hoặc trên một nhánh phát triển riêng làm việc trên phiên bản chính tiếp theo.

###Nếu ngay cả những thay đổi ngược không tương thích nhỏ nhất với API công khai cũng yêu cầu một phiên bản chính, thì tôi có thể kết thúc với phiên bản 42.0.0 không?
Đây là một câu hỏi về phát triển có trách nhiệm và tầm nhìn. Những thay đổi không tương thích không nên được đưa vào một cách dễ dàng cho phần mềm có nhiều mã phụ thuộc. Chi phí phải chịu để nâng cấp là đáng kể. Phải vượt qua các phiên bản chính để phát hành các thay đổi không tương thích có nghĩa là bạn sẽ suy nghĩ thông qua tác động của các thay đổi và đánh giá tỉ lệ/lợi ích liên quan.

###Tài liệu cho toàn bộ các API công khai là quá nhiều việc?
Nó là trách nhiệm của bạn như là một nhà phát triển chuyên nghiệp đối với tài liệu phần mềm phù hợp được sử dụng bởi người khác. Quản lý sự phức tạp của phần mềm là một phần cực kỳ quan trọng để giữ cho dự án hiệu quả, và điều đó khó thực hiện nếu không ai biết cách sử dụng phần mềm của bạn, hoặc phương pháp nào là an toàn để gọi. Về lâu dài đánh số phiên bản và sự nhấn mạnh vào API công khai được xác định rõ có thể giữ cho mọi người và mọi thứ được hoạt động trơn tru.

###Tôi phải làm gì nếu tôi vô tình phát hành một phiên bản nhỏ không tương thích ngược?
Ngay khi bạn nhận ra rằng bạn đã phá vỡ thông số đánh số phiên bản, sửa chữa vấn đề và phát hành một phiên bản phụ mới để khắc phục sự cố và khôi phục tính tương thích ngược. Ngay cả trong trường hợp này, nó là không thể chấp nhận cho việc sửa đổi một phiên bản đã được phát hành. Nếu nó là thích hợp, viết tài liệu phiên bản lỗi và thông báo người dùng của bạn về vấn đề này để họ biết về phiên bản lỗi.

###Tôi nên làm gì nếu tôi cập nhật các phụ thuộc của mình mà không thay đổi API công khai?
Điều đó sẽ được coi là tương thích vì nó không ảnh hưởng đến API công khai. Phần mềm rõ ràng phụ thuộc vào cùng các phụ thuộc như gói của bạn nên có thông số kỹ thuật riêng và tác giả sẽ lưu ý bất kỳ các xung đột nào. Việc xác định thời điểm để thay đổi một cấp độ bản vá hoặc là một phiên bản phụ tùy thuộc vào thời điểm bạn cập nhật các phụ thuộc của mình như là một bản vá lỗi hoặc giới thiệu một chức năng mới. Tôi mong đợi mã thêm vào cho trường hợp sau, trong trường hợp này nó rõ ràng là một phiên bản nhỏ tăng dần.

###Điều gì xảy ra nếu tôi thay đổi API công khai theo cách không tuân thủ thay đổi số phiên bản(tức là mã giới thiệu không chính xác là một thay đổi lớn nằm trong một bản vá được phát hành)?
Sử dụng phán đoán tốt nhất của bạn. Nếu bạn có một lượng lớn khá giả ảnh hưởng mạnh mẽ bằng cách thay đổi hành vi trở lại với những gì API công khai dự định, thì tốt nhất trong trường hợp này là thực hiện một phiên bản chính, mặc dù những sửa chữa có thể cân nhắc nghiêm túc như một bản vá. Nhớ rằng, đánh số phiên bản là tất cả về việc truyền đạt ý nghĩa bằng cách thay đổi số phiên bản. Nếu những thay đổi này quan trọng với người sử dụng của bạn, hãy sử dụng số phiên bản để thông báo cho họ.

###Tôi nên làm thế nào với những chức năng không còn được dùng nữa?
Những chức năng hiện có không còn dùng nữa là một phần bình thường của việc phát triển phần mềm và thường yêu cầu để làm phần mềm tốt hơn. Khi bạn không còn dùng một phần của API công khai của mình, bạn nên làm hai việc: (1) cập nhật tài liệu của bạn cho người dùng biết về thay đổi của bạn, (2) đề xuất phát hành một phiên bản phụ mới với phần không còn dùng nữa. Trước khi bạn loại bỏ hoàn toàn một chức năng không còn dùng nữa trong phiên bản phát hành chính thức, nên có ít nhất một phiên bản phát hành phụ có chứa phần không còn dùng nữa để người dùng có thể chuyển đổi dễ dàng sang API mới.

###đánh số phiên bản có giới hạn kích thước trên chuỗi phiên bản hay không?
Không, nhưng sử dụng phán đoán tốt. Ví dụ, một chuỗi phiên bản 255 ký tự là quá mức cần thiết. Ngoài ra các hệ thống cụ thể cũng có thể có giới hạn riêng của chúng đối với kích thước của chuỗi.

Về tôi
---
Đặc điểm kỹ thuật của đánh số phiên bản được viết bởi [Tom Preston-Werner](http://tom.preston-werner.com/), người sáng lập của Gravatars và đồng sáng lập GitHub.

Nếu bạn muốn để lại một phản hồi, làm ơn [mở một vấn đền trên GitHub](https://github.com/semver/semver/issues)

Giấy phép
---
[Creative Commons ― CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)
