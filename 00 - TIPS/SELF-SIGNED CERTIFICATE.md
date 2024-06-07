> Tạo CA Private Key

> 1. Đầu tiên, bạn tạo khóa riêng cho CA:

```shell
openssl genpkey -algorithm RSA -out ca-privkey.pem -pkeyopt rsa_keygen_bits:2048
```

> 2. bạn tạo chứng chỉ cho CA, tự ký chứng chỉ này (self-signed CA certificate). Chứng chỉ này có thể có thời hạn dài, ví dụ 10 năm (3650 ngày):

```shell
openssl req -new -x509 -days 3650 -key ca-privkey.pem -out ca-bundle.crt
```
> Bạn sẽ cần nhập thông tin cho CA như khi tạo CSR ở phần trước.

> 3. Tạo Private Key cho Server/Domain/Client
```shell
openssl genpkey -algorithm RSA -out privkey.pem -pkeyopt rsa_keygen_bits:2048
```

> 4. Tạo Certificate Signing Request (CSR) cho Server/Domain/Client
```shell
openssl req -new -key privkey.pem -out certificate.csr
```

> 5. Ký CSR bằng CA để tạo Server Certificate. Sử dụng CA certificate và CA private key để ký CSR và tạo chứng chỉ cho server. Chứng chỉ này có giá trị trong 1 năm (365 ngày):
```shell
openssl x509 -req -days 365 -in certificate.csr -CA ca-bundle.crt -CAkey ca-privkey.pem -CAcreateserial -out certificate.crt
```
> Lệnh trên sẽ tạo thêm một file certificate.srl dùng để lưu số serial của chứng chỉ CA.


> Các file kết quả

1. ca-privkey.pem: Khóa riêng của CA.
2. ca-bundle.crt: Chứng chỉ CA (self-signed).
3. privkey.pem: Khóa riêng của server.
4. certificate.csr: Certificate Signing Request của server.
5. certificate.crt: Chứng chỉ của server, được ký bởi CA.

> Bây giờ, bạn có thể sử dụng ca-bundle.crt để xác thực các chứng chỉ được CA của bạn ký (như certificate.crt).
