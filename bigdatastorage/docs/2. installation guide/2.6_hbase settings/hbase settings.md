# 2.6 Hbase 및 Phoenix 서버 설치

## 2.6.1 Hbase와 Phoenix
Phoenix 서버는 NoSQL의 한 종류인 Hbase 위에 관계형 데이터베이스에서 사용하는 SQL Layer를 구현한 오픈 소스 개발도구로, Hbase에 데이터를 적재할 때 Phoenix 서버를 거쳐서 처리되기 때문에 Hbase 구성시에는 Phoenix 서버를 함께 구성해야 합니다. 

<br/>

## 2.6.2 Hbase 및 Phoenix 서버 설치 

본 매뉴얼은 하기의 Hbase와 Phoenix 서버의 버전을 기준으로 작성하였습니다.

```
Phoenix  v5.1 
Hbase    v2.4.17 
```

Hbase와 Phoenix 서버를 구성할 때에는 상호 호환되는 버전을 사용해야 합니다. 호환 버전은 아래 Apache Phoenix 다운로드 페이지를 참고해주시기 바랍니다. <br/>

`참고)` Apache Phoenix Download : [https://phoenix.apache.org/download.html](https://phoenix.apache.org/download.html)

본 설치 메뉴얼에서는 Hbase Standalone으로 구성되는 설치 가이드만 제공합니다. Standalone으로 구성할 경우 Zookeeper는 Hbase 설치 시 자동으로 구성됩니다. 만약 사용하고 있는 Hbase db가 존재하는 경우, 아래 `2.6.2.1 Hbase` 설정은 제외하고 `2.6.2.2 Phoenix` 설정만 진행하도록 합니다. 
<br/>

### 2.6.2.1 Hbase

<br/>

- Hbase 다운로드 및 압축해제

    ```bash
    # /usr/local/lib 하위 경로에 Hbase tar 파일 다운로드
    cd /usr/local/lib
    wget http://apache.mirror.cdnetworks.com/hbase/2.4.17/hbase-2.4.17-bin.tar.gz
    tar -zxvf hbase-2.4.17-bin.tar.gz 
    ```

- 압축해제 디렉토리의 이름 변경

    ```bash
    mv hbase-2.4.17 hbase
    ```

- Hbase 환경변수 등록

    ```bash
    vi ~/.bash_profile

    # 하기 HBASE_HOME 환경변수를 .bash_profile 파일 내 선언
    export HBASE_HOME=/usr/local/lib/hbase

    source ~/.bashrc
    ```

- *[Optional] Hbase-site.xml 설정*
  - **Hbase Standalone 설치 시, 해당 Hbase-site.xml 설정은 별도로 진행하지 않아도 됩니다.**
  - Hbase-site.xml 경로는 `$HBASE_HOME/conf/hbase-site.xml` 에서 진행
  - 하기의 Property List는 참고용으로 일부 설정 값만을 기재해 놓은 것이며 설치자의 환경에 따라 설정 값을 추가하거나 다르게 설정할 수 있습니다.
  - 상세 설정은 하기의 `참고) Hbase Github`를 참고

<div align="center"><b>Hbase-site Property List</b></div>

  |Property|Description|Default Value| 
  |--------|-----------|-------------|
  |hbase.cluster.distributed|Hbase Cluster 구성 여부|false|
  |hbase.tmp.dir|로컬 파일 시스템의 임시 디렉토리 위치|./tmp|
  |hbase.rootdir|Hbase Region Server가 공유하는 디렉토리|-|
  |hbase.zookeeper.quorum|Zookeeper 사용 시, 서버 목록|-|
  |hbase.zookeeper.property.clientPort|zoo.cfg에 정의된 zookeeper client가 연결할 포트|-|
  |zookeeper.znode.parent|Zookeeper의 Root ZNode 설정|-|

`참고)` Hbase Github : [https://github.com/apache/hbase/blob/master/hbase-common/src/main/resources/hbase-default.xml](https://github.com/apache/hbase/blob/master/hbase-common/src/main/resources/hbase-default.xml)


<br/>

### 2.6.2.2 Phoenix

<br/>

- `phoenix-server-hbase-2.4-5.1.2.jar` 파일 다운로드

    ```bash
    wget https://repo1.maven.org/maven2/org/apache/phoenix/phoenix-server-hbase-2.4/5.1.2/phoenix-server-hbase-2.4-5.1.2.jar
    ```

- hbase 디렉토리 내 lib 디렉토리 하위로 복사

    ```bash
    cp phoenix-server-hbase-2.4-5.1.2.jar $HBASE_HOME/lib/
    ```

- Hbase 재시작
    ```bash
    $HBASE_HOME/bin/start-hbase.sh
    ```
