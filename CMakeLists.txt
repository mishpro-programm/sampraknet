cmake_minimum_required(VERSION 3.30)

project(raknet)

add_library(raknet STATIC
	src/BitStream.cpp
	src/CheckSum.cpp
	src/DataBlockEncryptor.cpp
	src/DS_HuffmanEncodingTree.cpp
	src/GetTime.cpp
	src/InternalPacketPool.cpp
	src/NetworkIDGenerator.cpp
	src/NetworkTypes.cpp
	src/PluginInterface.cpp
	src/RakClient.cpp
	src/RakPeer.cpp
	src/RakServer.cpp
	src/RakSleep.cpp
	src/Rand.cpp
	src/ReliabilityLayer.cpp
	src/rijndael.cpp
	src/RPCMap.cpp
	src/samp_auth.cpp
	src/samp_netencr.cpp
	src/SAMPRPC.cpp
	src/SHA1.cpp
	src/SimpleMutex.cpp
	src/SocketLayer.cpp
	src/StringCompressor.cpp
	src/StringTable.cpp
)

if(WIN32)
	target_compile_definitions(raknet PRIVATE _CRT_SECURE_NO_WARNINGS _WINSOCK_DEPRECATED_NO_WARNINGS)
	target_link_libraries(raknet PRIVATE ws2_32)
endif()
target_include_directories(raknet PUBLIC include)