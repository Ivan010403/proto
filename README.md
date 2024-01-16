# Protocol Buffers (Protobuf)

Для общения gRPC клиента и gRPC сервера необходим API контракт. Благодаря поддержке множества языков программирования (контракт имеет одну структуру с разной реализацией на разных яызках) это делает gRPC подход к разработке очень гибким. По условию тестового задания надо было реализовать 3 процесса:

1. Передача бинарного файла (изображения) от gRPC клиента к gRPC серверу. Этим занимается:

```rpc UploadFile (stream UploadFileRequest) returns (UploadFileResponce)```

Заметим, что объём файла может быть слишком большим, и поэтому мы вынуждены использовать технологию streaming и фрагментировать наши данные, передавая их по частям (client-side streaming)

2. Передача бинарного файла (изображения) от gRPC сервера к gRPC клиенту. Этим занимается:

```rpc GetFile (GetFileRequest) returns (stream GetFileResponce)```

Поток данных развёрнут в сторону клиента (server-side streaming)

3. Иметь возможность посмотреть все файлы, которые сейчас хранятся на диске. Этим занимается:

```rpc GetFullData (GetFullDataRequest) returns (stream GetFullDataResponce)```

И снова мы вынуждены использовать потоковую передачу

4. Также я возможность удалить файл используя унарный вызов:

```rpc DeleteFile (DeleteFileRequest) returns (DeleteFileResponce)```
