# Tìm hiểu về hping3

# Mục lục

- [1. hping3 là gì?](#1)
- [2. Chức năng của hping3](#2)
- [3. Cách sử dụng hping](#3)
    - [3.1 Base options](#31)
    - [3.2 Protocol selection](#32)

<a name="1"></a>

## 1. hping3 là gì?
Hping3 - Công cụ quét mạng và máy phân tích cho giao thức TCP/IP được phân phối bởi Salvatore Sanfilippo (còn được gọi là Antirez).

Nó là một loại của một thửu nghiệm cho an ninh mạng. Nó là một trong những `defacto` cong cụ để kiểm tra an nih và thử nghiệm tường lửa.

Công cụ quét mạng hping là một bộ phân tích, phân tích gói tin TCP/IP theo định hướng dòng lệnh. Giao diện được lấy cảm ứng từ lệnh ping(8) Unix, nhưng hping không chỉ có thể gửi các yêu cầu echo ICMP. Nó hỗ trợ giao thức TCP, UDP, ICMP và RAW-IP, có chế độ traceroute, khẳ năng gửi tập tin giữa một kênh được bảo vệ và nhiều tính năng khác.

Trong khi hping chủ yếu được sử dụng như một Công cụ quét mạng trong quá khứ, nó có thể được sử dụng theo nhiều cách bởi những người không quan tâm đến bảo mật để kiểm tra mạng và máy chủ.

<a name="2"></a>

## 2. Chức năng của hping3

- Kiểm tra tưởng lửa, quy tác tưởng lửa
- Quets cổng nâng cao
- Thử nghiệm mạng, sử dụng các giao thức khác nhau, TOS, phân mảnh
- Manual path MTU discovery
- Traceroute nâng cao trong tất cả các giao thức đươc hỗ trợ
- Quest dấu vân tay từ xa
- Đoán thời gian hoạt động từ xa
- TCP/IP stacks auditing
- hping cũng có thể hữu ích cho sinh viên đang học TCP / IP.
- Kiêm tra IDS

<a name="3"></a>

## 3. Cách sử dụng

- Sử dụng:

```
hping3 --h
```

![Imgur](https://i.imgur.com/bXcZwS5.png)

<a name="31"></a>

## 3.1 Base options

- -c --count: Dừng lại sau khi đã *count* response packets
- -i --interval: Chỉ rõ khoảng thời gian tính bằng giây hoặc ms giữa những lần gửi packet. `--X` set wait X seconds, --interval `uX` set wait X ms. Mặc định là 1s mỗi lần gửi 1 packet
- --fast: Alias for -i u10000. Hping will send 10 packets for second.
- --faster: Alias for -i u1. Nhanh hơn --fast
-- flood: Gửi gới tin ngay lập tức, không cần quan tâm tới các bản tin reply trả lại 



<a name="32"></a>

### 3.2 Protocol selection

Giao thức mặc định là TCP, hping3 sẽ gửi tiêu đề tcp tới port 0 của target host 
- -0 --rawip: RAW IP mode, hping3 sẽ gửi IP header với data kèm theo đó --signature và --file, xem thêm --protocol cho phép thiết lập truowgf giao thức
- -1 --icmp: ICMP mode, hping3 gửi ICMP echo-request, có thể set thêm type/code sử dụng `--icmptype --icmpcode`
- -2 --udp: UDP mode, hping3 send udp to target port 0
- -8 --scan: Tùy chọn này mô tả 1 group port để scan
Ví dụ:

```
hping3 --scan 1-1000,8888,known -S target.host.com

# Câu lệnh trên mô tả scan port từ 1 tới 1000, port 8888 và tất cả các port liệt kê trong /etc/services
```

![Imgur](https://i.imgur.com/iCFhd0J.png)

Ví dụ khác:

```
hping --scan '1-1024,!known' -S target.host.com
```

- -9 --listen signature: HPING3 listen mode, using this option hping3 waits for packet that contain signature and dump from signature end to packet's end. For example if hping3 --listen TEST reads a packet that contain 234-09sdflkjs45-TESThello_world it will display hello_world.