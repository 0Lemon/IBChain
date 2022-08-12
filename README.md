# IBChain
服务器：Centos7；配置打开22、8545、30303端口

安装必须环境 yum update -y && yum install git wget bzip2 vim gcc-c++ ntp epel-release nodejs tree -y

打开防火墙 
firewall-cmd --zone=public --add-port=8545/tcp --permanent
防火墙-cmd --zone=public --add-port=30303/tcp --permanent
防火墙-cmd --reload

上传geth-alltools-linux-amd64-1.9.24-cc05b050.tar.gz

解压tar -zxvf geth-alltools-linux-amd64-1.9.24-cc05b050.tar.gz

进入geth-alltools-linux-amd64-1.9.24-cc05b050

将下面的文件复制到/usr/local/bin
cp ./abigen /usr/local/bin/abigen
cp ./bootnode /usr/local/bin/bootnode
cp ./clef /usr/local/bin/clef
cp ./evm /usr/local/bin/evm
cp ./geth /usr/local/bin/geth
cp ./puppeth /usr/local/bin/puppeth
cp ./rlpdump /usr/local/bin/rlpdump

测试geth是否可用geth版本

创建节点文件夹 mkdir -p Ibchain/node

创建节点区块链地址 
cd IB链
geth --datadir 节点/新帐户

将地址和密码保存至节点中
echo "node1的账户地址" >> accounts.txt
echo "账户密码" >> node/password.txt

将ibchain.json上传至服务/root/Ibchain目录下

初始化ibchain geth --datadir node init ibchain.json

打开剖析
geth --networkid 1308 --datadir 节点 --http --http.port 8545 --http.addr "0.0.0.0" --port 30303 --http.corsdomain "*" --nodiscover --http.api "db ,eth,net,web3,txpool,personal,miner" --unlock 0 --password ./node/password.txt --allow-insecure-unlock 控制台

执行添加节点命令查看是否同步区块
执行建议，等待通过查看是否参与验证
全部通过后执行下一步

通过守护程序启动IBChain，并将日志输入到1.log中
nohup geth --networkid 1308 --datadir 节点 --http --http.port 8545 --http.addr "0.0.0.0" --port 30303 --http.corsdomain "*" --nodiscover --http.api" db,eth,net,web3,txpool,personal,miner" --unlock 0 --password ./node/password.txt --allow-insecure-unlock no.log 2>&1 &

光盘~

进入 IBchain-Geth 分析 geth attach ./Ibchain/node/geth.ipc

加入IBChain网络
admin.addPeer("enode://5ae3e0abcae1fe3ee47b85bb546927c0326a3f736d3231d0a85c498a29143dd2320d89b8332cce6bada2f81da1aa096d48a36a3b24a737ae91a4ddad10852215d@976.)

提出建议
clique.propose("节点账户地址",true)

等待同意建议

加入成功

开启验证 miner.start(2)

Ctrl+D 出口分析
--
