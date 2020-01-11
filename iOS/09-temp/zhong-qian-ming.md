
#通过指令修改渠道 id 重签名


```Swift

# 指令打包ipa 子包

# 遍历修改代理 id + 打包
#列出所有开发者证书文件：
security find-identity -p codesigning -v
#找到开发者签名
nwfSign='08E07AF463F795D7C7CFA5100597E52D05AEC773'
#根据 对应APP id 的描述文件 embedded.mobileprovision 生成 profile.plist 文件
security cms -D -i embedded.mobileprovision  > profile.plist
#根据 profile.plist 生成 entitlements.plist
/usr/libexec/PlistBuddy -x -c 'Print :Entitlements' profile.plist > entitlements.plist

#需要配置的变量
#产品名称
productName= '' #'E04_'
#绝对路径
pathFirst='/Users/dwight/Desktop/tabletest'
#执行文件
nwfExecutableFile='NWF'
#包文件
payAppDirectory='/Payload/NWF.app'
#存放子包的文件夹
subPackage='package'
mkdir ${subPackage}


#代理文件
agentSignFile='/AgentSign.plist'

for line in $(cat channelID.txt)
do
	#修改代理 id
	agentId=`echo $line|cut -f1 -d';'`
	#targetName=`echo tabletest_${agentId}`
	echo "agentId=$agentId"
	/usr/libexec/PlistBuddy -c "Set agentId $agentId" ${pathFirst}${payAppDirectory}${agentSignFile}

	#创建新的文件夹
    mkdir ${subPackage}/${agentId}

	#移除签名文件夹
	rm -rf ${pathFirst}${payAppDirectory}/_CodeSignature

	#重新签名库 framework  dylib
	for file in  ${pathFirst}${payAppDirectory}/Frameworks/*
	do
		#echo "file=$file"
		/usr/bin/codesign --force --sign ${nwfSign} --entitlements entitlements.plist ${file}
	done

	#重新签名执行文件
	/usr/bin/codesign --force --sign ${nwfSign} --entitlements entitlements.plist ${pathFirst}${payAppDirectory}/${nwfExecutableFile}

	#打包
	targetName=`echo ${productName}${agentId}`
	zip -r "${subPackage}/${targetName}.ipa" Payload
done



```
