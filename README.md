# RxSocketClient

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/codeestX/RxSocketClient/pulls)[![API](https://img.shields.io/badge/API-20%2B-brightgreen.svg)](https://android-arsenal.com/api?level=20)[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

RxSocketClient, Reactive Socket APIs for Android, Java and Kotlin, powered by RxJava2
RxSocketClient，支持Android，Java和Kotlin的响应式Socket APIs封装，基于RxJava2

RxJava2 Version: 2.1.1

# Usage

### init
```
SocketClient mClient = RxSocketClient
        .create(new SocketConfig.Builder()
                .setIp(IP)
                .setPort(PORT)
                .setCharset(Charsets.UTF_8)
                .setThreadStrategy(ThreadStrategy.ASYNC)
                .setTimeout(30 * 1000)
                .build())
        .option(new SocketOption.Builder()
                .setHeartBeat(HEART_BEAT, 60 * 1000)
                .setHead(HEAD)
                .setTail(TAIL)
                .build());

```
| value | default | description |
| :--: | :--: | :--: |
| Ip | required | host address |
| Port | required | port number |
| Charset | UTF_8 | the charset when encode a String to byte[] |
| ThreadStrategy | Async | sending data asynchronously or synchronously|
| Timeout | 0 | the timeout of a connection, millisecond |
| HeartBeat | Optional | value and interval of heartbeat, millisecond |
| Head | Optional | appending bytes at head when sending data, not included heartbeat |
| Tail | Optional | appending bytes at last when sending data, not included heartbeat |

### connect
```
Disposable ref = mClient.connect()
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new SocketSubscriber() {
                    @Override
                    public void onConnected() {
                        Log.e(TAG, "onConnected");
                    }

                    @Override
                    public void onDisconnected() {
                        Log.e(TAG, "onDisconnected");
                    }

                    @Override
                    public void onResponse(@NotNull byte[] data) {
                    	// receive data
                        Log.e(TAG, Arrays.toString(data));
                    }
                });
```

### disconnect
```
mClient.disconnect();
//or
ref.dispose();
```

### sendData
```
mClient.sendData(bytes);
//or
mClient.sendData(string);
```

# License

      Copyright (c) 2017 codeestX

      Licensed under the Apache License, Version 2.0 (the "License");
      you may not use this file except in compliance with the License.
      You may obtain a copy of the License at

         http://www.apache.org/licenses/LICENSE-2.0

      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
      See the License for the specific language governing permissions and
      limitations under the License.
