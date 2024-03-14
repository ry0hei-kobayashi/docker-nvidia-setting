# Docker build時にnvidia関連を有効にする方法

Created: 2023年5月25日 19:44
Last edited time: 2024年3月14日 20:56
Course: 設定TIPS
Created by: Arata Sakamaki
Last edited by: Ryohei Kobayashi

/etc/daemon/docker.jsonを以下のように変更する．

docker runするときに—gpus all オプションがなくても自動的にGPUが割当たるようになる

```json
$ cat /etc/docker/daemon.json 
{
    "default-runtime": "nvidia",  # <-追加
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}
```

上記の一行を追加後以下のコマンドを打つことでdocker enginを再起動する．

```jsx
sudo service docker restart
```

docker build時にもnvidiaやcuda関係をつけたいときは

```bash
DOCKER_BUILDKIT=0 docker build 
DOCKER_BUILDKIT=0 docker compose bulid
```

のように環境変数を設定することで読み込ませることができる
