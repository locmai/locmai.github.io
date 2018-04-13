---
layout: post
title: "Zalo Hackathon 2017 - AI Challenges"
date: 2018-04-13
excerpt: "A Hackathon organized by Zalo - Solving problems with AI, AR and IoT"
tags: [hackathon]
feature: https://i.imgur.com/Gyr4bw4.jpg
comments: true
---

# Zalo Hackathon 2017 - AI Challenge

Bài viết này mình chia sẻ lại một phần trải nghiệm kì Hackathon với nội dung về ứng dụng AI của Zalo gần cuối năm 2017.

Do mình có share một bài blog diễn biến cụ thể rồi nên trong bài này mình chỉ tập trung về cách tổ chức, trải nghiệm so với những kì Hackathon khác mà mình từng tham gia.

## Khởi đầu

Vòng gửi xe của Zalo thì cũng không có gì khó khăn lắm. Tụi mình có một tuần để chuẩn bị một ý tưởng bất kì và biện luận với ban giám khảo. Tụi mình có một ý tưởng gợi ý nhạc thông qua mạng lưới Zing MP3 dựa trên thói quen nghe nhạc của người dùng và nhận diện những ca sĩ được yêu thích nhiều. 

OK. Đó là vòng loại. 

<figure>
	<img src="https://i.imgur.com/fTgPOdl.jpg">
	<figcaption>Team Đường xinh đẹp chính thức tham gia Zalo Hackathon.</figcaption>
</figure>

Điểm thú vị ở kì Hackathon này chính là đề bài cụ thể chỉ được đưa ra tới khi Hacking day bắt đầu, còn lại tất cả các team chỉ biết nội dung tổng quát là ứng dụng AI,AR và IoT. Một lát nữa mình sẽ đi sâu hơn, còn bây giờ thì tới phần quan trọng nhất của những cuộc thi Hackathon ... đồ ăn

## Đồ ăn

Mục đích chính khi tham gia những cuộc thi Hackathon, buổi sáng trước khi bắt đầu cuộc thi, Ban Tổ chức chuẩn bị sẵn một tiệc trà. Đại khái có các thứ như Trà, cà phê, sữa tươi và nước ngọt, đồ ăn thì sẽ có các món snack, bánh mì các loại. Đại khái là mình chưa cần biết chuyện gì sẽ xảy ra, nhưng cứ bốc trước một núi đồ ăn sáng về vị trí của team rồi thưởng thức buổi sáng.

Tầm giờ trưa thì có các phần cơm gà / bò / xá xíu. 

<figure>
	<img src="https://i.imgur.com/FDKm0aR.jpg">
	<figcaption>Team mình chuẩn bị ăn trưa.</figcaption>
</figure>

Sau đó thì tại các bàn bày đồ ăn cũng có tráng miệng như trái cây.

<figure>
	<img src="https://i.imgur.com/EY2gOnt.jpg">
	<figcaption>Căng da bụng, trùng da mắt ...</figcaption>
</figure>

Từ chiều tới tối thì cũng có phần cơm như bữa trưa và bàn đồ ăn thì vẫn đầy ắp bánh mì, nước uống đủ loại.

Đến khuya thì có mì ly, xúc xich và đủ loại đồ ăn khuya thú vị khác.

So với Facebook Hackathon thì kì này không hoành tráng bằng, nhưng đồ ăn lại khá thú vị và đủ loại. Ban Tổ chức có vẻ nắm rõ tâm lý người tham gia khi chuẩn bị khá đầy đủ và phù hợp với các thời điểm nhất định.

OK. Tạm gác lại đồ ăn. Let's the hacking ... begin

## Hacking day

Như mình nói ở trên thì đề bài chỉ được phát ngay lúc cuộc thi bắt đầu. Ở đây, Zalo / VNG đã chuẩn bị hẳn 8 chủ đề riêng biệt là những vấn đề thực tế có thể áp dụng Machine Learning, đồng thời với mỗi bài toán mà họ đề ra sẽ có gắn kèm một tập dữ liệu liên quan - lấy từ thực tế. 

Đúng như dự đoán. Có 2 đề bài ứng dụng ML là Music Recommendation và Music Classification. 

Định hướng của team mình: Việc phân loại nhạc có thể sử dụng để đề xuất nhạc cho người dùng, nếu suy luận rằng người dùng thích nghe một bài nhạc vì âm hưởng của nó thì khi phân tích được một bài nhạc có cùng âm hưởng và dựa trên đó đưa ra dự đoán. OK. Quá hoàn hảo, nếu có thể đi theo hướng đó, mình có thể dùng tập dữ liệu của cả hai đề bài để giải quyết tốt nhất cho một. Team mình quyết định chọn Music Recommendation theo hướng giải quyết trên.

Hai tập dữ liệu cho 2 bài: Danh sách 30,000 bài nhạc (Có link, thể loại, tên nghệ sĩ,etc) cho bài toán Music Classification và danh sách lượt nghe của người dùng (tầm 1 triệu dòng) cho bài toán Music Recommendation. Toàn bộ là dữ liệu thật từ Zing MP3. 

Công việc đầu tiên, trích một lượng nhỏ các bài hát nằm trong danh sách lượt nghe. Dĩ nhiên là mình không thể crawl hết 30,000 bài một lúc và trích xuất đặc tính từng bài từ đó ngay tức khắc được. Đồng thời Hackathon là một cuộc thi có giới hạn về thời gian, dữ liệu càng nhiều, thời gian train model sẽ càng lâu. 

Trong lúc đó mình thử nghiệm hướng đi đầu tiên: Phân tới tầng phổ quang của một file audio. Đại khái là từ một bản audio, có thể trích xuất các điểm về tầng suất theo giai đoạn. OK, mình google một vòng một số thư viện đã implement sẵn của các công ty lớn và đại học. Viết một wrapper method ngắn để extract vừa đủ. Thử với một file audio có thời lượng 10 giây ... mất hết 26 giây. Vấn đề đầu tiên bắt đầu từ đây. Với một bản nhạc bình quân sẽ có thời lượng là 3 phút, vậy team mình sẽ mất hết 468 giây ~ 7.8 phút cho việc rút trích đặc tính của một bài nhạc. Chưa tính tới thời gian train model.

Tới thời điểm này thì có các Mentors từ VNG trợ giúp, họ nghe thử hướng đi của nhóm mình và đưa ra vài lời khuyên khá bổ ích. Về việc rút trích đặc tính từ phổ quang, khả năng thực hiện được là có nhưng trong thời gian cuộc thi thì sẽ là bất khả thi. Họ cũng gợi ý một số phương thức để việc rút trích đó nhanh hơn nhưng nó cũng sẽ không thực sự hiệu quả.

Do đó team mình đã phải bắt đầu chuyển hướng. OK. Vậy đi từ hướng đơn giản trước hết: Các ca sĩ, thể loại mà người nghe yêu thích. Một trong những đặc tính dễ lấy nhất và cũng dễ đánh trọng số nhất. Việc xử lý đống data này bắt đầu gặp vấn đề khi một số dòng dữ liệu có ô null (đôi khi một người uplaod một bài nhạc lên Zing MP3, họ quên/không thêm tên ca sĩ hay thể loại). Dẫn tới việc từ 1 triệu dòng dữ liệu, team mình chỉ xử lý và scope nhỏ lại xuống 100,000 dòng xử dụng được và xem nó như mẫu thử.

Tiếp theo, sử dụng thời gian nghe và thời điểm nghe cũng là một cách. Team mình nhanh chóng đưa 2 món đó vào danh sách Feature và xử lý nhanh từ đống dữ liệu.

Team xử lý ma trận xong train trực tiếp trên máy xuyên đêm. Đến sáng thì mình lo chuẩn bị một web app đơn giản để demo khả năng gợi ý nhạc và chuẩn bị slide cho buổi trình bày trước Ban giám khảo.

Đại khái thì hết phần thi. Cũng khá mệt mỏi vì một đêm không ngủ. Team mình cũng hoàn thành khá tốt phần trình bày trước hội đồng giảm khảo

<figure>
	<img src="https://i.imgur.com/3okk2GJ.jpg">
	<figcaption>Đuối như trái chuối.</figcaption>
</figure>

Đến cuối cũng rinh được một giải nhỏ đem về

<figure>
	<img src="https://i.imgur.com/GOXnrIf.jpg">
	<figcaption>Giải triển vọng :D</figcaption>
</figure>

Định viết thêm vài dòng nhận xét khá chi tiết nhưng bài cũng dài nên mình tóm gọn lại, kì thi này BTC đã thực hiện tốt, Ban giám khảo có tính chuyên môn cao, đội Mentor tận tình và khâu chuẩn bị kĩ lưỡng.

Tới cuối ngày, sau buổi thi thì Zalo mở tiệc Pizza với Budweiser quẩy banh nóc. Nói chung là Zalo đầu tư phần này ổn quá nên mình cũng không biết chê vào đâu nữa T_T

Viết tới đây thôi, lười viết thêm quá, cũng không còn gì nhiều, đại khái thì kì thi vừa qua mình cũng có trải nghiệm khá thú vị nhờ Zalo và các thành viên trong team :D.