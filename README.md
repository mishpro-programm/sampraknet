# SA:MP compatible modification of RakNet

This RakNet modification contains code that allows it to encode/decode SA:MP datagrams and handle SA:MP queries

# CMake
If you want to include this library to your CMake project you can do it this way:
```cmake
include(FetchContent)
FetchContent_Declare(sampraknet
  GIT_REPOSITORY https://github.com/mishpro-programm/sampraknet
  GIT_TAG v1.0
)
# here goes your options
FetchContent_MakeAvailable(sampraknet)

target_link_libraries(your_target PRIVATE raknet)
```

List of available options:
```text
RAKNET_DLL (ON/OFF) - Build RakNet as shared library (Default: OFF)
RAKNET_THREADSAFE (ON/OFF) - Build threadsafe variant of RakNet (Default: OFF)
```

# Added stuff
```c++
SAMPQuery* RakServerInterface::ReceiveSAMPQuery();

enum SAMPQueryType : unsigned char {
	ClientList = 0x63,
	PlayerInfo = 0x64,
	ServerInfo = 0x69,
	Ping = 0x70,
	RulesList = 0x72,
	RCONCmd = 0x78,
};
struct SAMPQuery {
	SAMPQueryType type;
	char* data;
	int dataLength;
	unsigned int targetAddress;
	unsigned short targetPort;
	sockaddr_in senderAddress;
	SOCKET socket;
	RakPeer* receiver;
	~SAMPQuery();
	void SendResponse(char* data, int len);
};
```

# Credits
[YashasSamaga/RakSamp](https://github.com/YashasSamaga/RakSamp) for reverse engineering SA:MP network encryption code
