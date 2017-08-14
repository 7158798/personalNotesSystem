

BafSchedulerJob.java

PasApplicationListener,java



public class BafSchedulerJob implements org.quartz.Job {





LastSuccessDate:

LastSuccessJobKey:

jobIntervalUnit:



新建了一个public abstract class AbstractCommonCommand implements BafJobCommand {

来对应这种通用型 不查询 常用性服务





熟悉一下框架里的东西

尽快

后面还有一个job

巩固和联系

所以这个要尽快。





## Quartz教程

Quartz是一个开源的作业调度框架，可以让计划的程序任务一个预定义的日期和时间运行。Quartz可以用来创建简单或复杂的日程安排执行几十，几百，甚至是十万的作业数。

Apache License  Version 2.0, January 2004

[http://www.apache.org/licenses/](http://www.apache.org/licenses/)

Quartz 是一种功能丰富的，开放源码的作业调度库，可以在几乎任何Java应用程序集成 - 从最小的独立的应用程序到规模最大电子商务系统。

Quartz可以用来创建简单或复杂的日程安排执行几十，几百，甚至是十万的作业数 -  作业被定义为标准的Java组件，可以执行几乎任何东西，可以编程让它们执行。

如果应用程序需要在给定时间执行任务，或者如果系统有连续维护作业，那么Quartz是理想的解决方案。









## 我们的quartz使用

```
public class BafSchedulerJob implements org.quartz.Job {
public static Logger logger = LoggerFactory.getLogger(NFSLogType.RECON);
public static Logger messageLogger = LoggerFactory.getLogger(NFSLogType.MESSAGE);
public void execute(JobExecutionContext context) throws JobExecutionException {
	try {
		executeInternal(context);
	} catch (Throwable ex) {
		logger.error("Failed to run job", ex);
		throw new JobExecutionException(ex);
	} finally {
		AiafContext.clear();
	}
}
```
com.mdiaf.batch.service：BafJobCommand.java,  BafSchedulerJob.java,  



FundTransAdapterCategory.java 里边的
```
@Override
public ShareBalanceQueryResponse shareBalanceQuery(ShareBalanceQueryRequest shareBalanceQueryRequest) throws Exception {
		return getAdapter(shareBalanceQueryRequest.getProductProviderCode()).shareBalanceQuery(shareBalanceQueryRequest);
	}
```
路由时 ，进入了下边的Mock状态，修改`Trade_Mock_Switch`（config Params 中{
"productProviderCode":"NFFUND",
"mockStatus":"InActive"
},）后好了。

```
boolean isMock = isMock(productProviderCode);
		if(isMock)
			return mockNffundFundTransAdapter;
		else {
			if (StringUtils.isBlank(productProviderCode))
				return nffundFundTransAdapter;

			switch (productProviderCode.toUpperCase()) {
			case "NFFUND":
				return nffundFundTransAdapter;
```





JobInstances(*) 中发现 “nf南方接口健康性检查” 在192.168.1.94（即我的饿主机IP地址）中运行status是Completed，在127.0.0.1以及其他IP地址均运行不成功。

在http://172.16.1.131:8080/aiaf/BmfAggrEditor/AdministrationModule?bmfAggrId=8773中 config params的TRIGGER_HOST的value是192.168.1.94。



#南	方每日上传文件检查

借鉴：
batch：
文件流动
BhlifeNewBusinessInJob
BhlifeNewBusinessInJobCommand，（implements BafJobCommand）
BhlifeNewBusinessOutJobCommand，(implements BafJobCommand)
报文上传下载
标准的规范化的

InsuranceNewBusinessInJobCommand，(extends InsuranceAbstractJobCommand  implements BafJobCommand)
标准的一套job 更标准化的 更规范化 
可以考虑供多个第三方金融机构调用
InsuranceNewBusinessOutJobCommand,   (extends InsuranceAbstractJobCommand implements BafJobCommand)

TaLifeInsRealTimeTrans
InsRealTimeTrans


南方每日上传文件检查
BafJobParameter Detail：JobParameters--
BafJobSchedule Summary
南方文件检查feature/jira/20170824/FC-388

WithdrawDelayCommand 

TransferUploadCommand

NFFundTransExtDepositUploadCommand



BatchManagerImpl.java--------runjob()

BafSchedulerJob.job----------





```
 [java] 遍历输出D盘文件夹中以a开头的txt文件,并且统计个数
package com.heima.bean;
import java.io.File;
import java.util.Scanner;

public class Demo3 {/** * @param args * 遍历输出D盘文件夹中以a开头的txt文件,并且统计个数 */
	public static void main(String[] args) {
		File dir=new File("D:\\"); //对象
		int num1=getNum(dir);
		System.out.println(num1);
	}
	//getNum方法获取统计个数
	public static int getNum(File dir) {
		int num=0;//用于统计数量
		File[] subfile =dir.listFiles();//获取所有文件
		if(subfile!=null){//判断是否为空,有些计算机,在C盘等盘符下,一些系统文件,禁止访问;不加这个,会报错
			for (File file : subfile) { //遍历获取每一个文件
				if(file.isFile() && file.getName().endsWith(".txt") &&file.getName().contains("a") && !(file.getName().charAt(0)+"").equals("a")){ //条件判断num++;//统计数量增加
					System.out.println(file);//输出满足条件的文件名
				}
				else if(file.isDirectory()){ //如果是文件夹
					num=num+getNum(file); //统计数量
				}
			}
		}
	return num; //返回值为数量
	}
}
```

```
1，连接
FundFileTransProcessServiceImpl.java
public void fundFileUpload(FileJobParameter jobParameter) throws Exception {
	// 3. 创建SFTP连接
	ChannelSftp channelSftp = fundJobGeneralService.createChannelSftp(fileTransBean);
	}
	@Override
	public ChannelSftp FundFileConnect(FileJobParameter jobParameter) throws Exception {
		log.info(jobParameter.getProductProviderCode()+"数据处理开始执行！");
		// 0. 配置初始化(包括文件配置、通信配置等).
		InsuranceFileTransBean fileTransBean = fundFileJobGeneralService.createFileTransBean(jobParameter);
		// 1. 创建SFTP连接
		ChannelSftp channelSftp = fundJobGeneralService.createChannelSftp(fileTransBean);
		return channelSftp;
	}
	
	
2，获取服务器目录
NFFundFileJobSupportProcess.java
@Service("nFFundFileJobSupportProcess")
public class NFFundFileJobSupportProcess implements FundFileJobGeneralService {
	@Override
	public InsuranceFileTransBean createFileTransBean(FileJobParameter jobParameter) throws Exception {
			//获取文件名
		log.info("文件名是:{}" ,localFileName);
		if (StringUtils.equals(fileOperateType, Constant.FILE_UPLOAD_PATH)) {
			localFileName = NfFundFileUtils.createUploadFileName(jobParameter.getMercId(), fileBusinessName, jobParameter.getJobInstKey(), Constant.NFFUND_RECONFILE_POSTFIX);
			
			//针对南方的特殊要求(反人类) 文件名和以前的规范不一样 需要特殊处理一下 20170622 zhushuai start
			if(StringUtil.equals(jobParameter.getBusinessType(),NFFileCategoryAndNameEnum.TRACE_FILE.getCategory()) ||
					StringUtil.equals(jobParameter.getBusinessType(),NFFileCategoryAndNameEnum.QUESTIONNAIRE_FILE.getCategory())){
				localFileName = jobParameter.getMercId() + "_" + jobParameter.getJobInstKey().split("-")[1].trim().substring(0, 8) + "_" + fileBusinessName + Constant.NFFUND_RECONFILE_POSTFIX;
			}
			//20170622 zhushuai end
			
			//获取本地保存路径
			localPath = NfFundFileUtils.getUploadLocalFilePath(ftpEndpoint, fileOperateType, jobParameter.getJobInstKey());
			log.info("保存本地的路径是:{}" ,localPath);
			//获取服务器目录
		    remotePath = NfFundFileUtils.getUploadRemoteFilePath(ftpEndpoint, fileOperateType, jobParameter.getJobInstKey());
			log.info("服务器目录是:{}" ,remotePath);
		}else{
			localFileName = NfFundFileUtils.createDownFileName(jobParameter.getMercId(), fileBusinessName, jobParameter.getJobInstKey(), Constant.NFFUND_RECONFILE_POSTFIX);
			//获取本地保存路径
			localPath = NfFundFileUtils.getDownLocalFilePath(ftpEndpoint, fileOperateType, jobParameter.getJobInstKey());
			log.info("保存本地的路径是:{}" ,localPath);
			//获取服务器目录
		    remotePath = NfFundFileUtils.getDownRemoteFilePath(ftpEndpoint, fileOperateType, jobParameter.getJobInstKey());
			log.info("服务器目录是:{}" ,remotePath);
		}
		
		
		fileTransBean.setFtpEndPoint(ftpEndpoint);
		fileTransBean.setStartDate(startDate);
		fileTransBean.setEndDate(endDate);
		fileTransBean.setLocalPath(localPath);
		fileTransBean.setRemotePath(remotePath);
		fileTransBean.setRemoteFileName(localFileName);
		fileTransBean.setLocalFileName(localFileName);
		fileTransBean.setQueryArgs(queryArgs);
		fileTransBean.setCommonSql(commonSql);
		fileTransBean.setHeadSql(headSql);
		fileTransBean.setBodySql(bodySql);
        fileTransBean.setOrmFileDataService(ormFileDataService);

		return fileTransBean;
		
		
		
3，进入服务器路径 remotePath

    /**
     * 链接linux
     * */
    public ChannelSftp connect() {
        ChannelSftp sftp = null ;
        try {
            JSch jsch = new JSch();
            jsch.getSession(username, host, port);
            sshSession = jsch.getSession(username, host, port);
            sshSession.setPassword(password);
            Properties sshConfig = new Properties();
            sshConfig.put("StrictHostKeyChecking", "no");
            sshSession.setConfig(sshConfig);
            sshSession.connect();
            LogManager.info(String.format("%s connect success" , host));
            Channel channel = sshSession.openChannel("sftp");
            channel.connect() ; 
            sftp = (ChannelSftp) channel;
        } catch (Exception e) {
            LogManager.err("connect:" + host , e ); 
            close( null );
            return null ; 
        }
        return sftp;
    }

    /**
     * linux上传文件
     * */
    public void upload(String directory,File file){
        ChannelSftp sftp = connect() ; 
        try {
            if(null != sftp){
                sftp.cd(directory);
                LogManager.info(String.format("cd %s" , directory));
                sftp.put(new FileInputStream(file), file.getName());
            }
        } catch (Exception e) {
            LogManager.err("upload:" + host , e ); 
        }finally{
            sftp.disconnect() ;
            sftp.exit();
            sshSession.disconnect();
        }
    }
   
   
4，计算remotepath目录下的.txt文件数量。
 [java] 遍历输出D盘文件夹中以a开头的txt文件,并且统计个数
package com.heima.bean;
import java.io.File;
import java.util.Scanner;

public class Demo3 {/** * @param args * 遍历输出D盘文件夹中以a开头的txt文件,并且统计个数 */
	public static void main(String[] args) {
		File dir=new File("D:\\"); //对象
		int num1=getNum(dir);
		System.out.println(num1);
	}
	//getNum方法获取统计个数
	public static int getNum(File dir) {
		int num=0;//用于统计数量
		File[] subfile =dir.listFiles();//获取所有文件
		if(subfile!=null){//判断是否为空,有些计算机,在C盘等盘符下,一些系统文件,禁止访问;不加这个,会报错
			for (File file : subfile) { //遍历获取每一个文件
				if(file.isFile() && file.getName().endsWith(".txt") &&file.getName().contains("a") && !(file.getName().charAt(0)+"").equals("a")){ //条件判断num++;//统计数量增加
					System.out.println(file);//输出满足条件的文件名
				}
				else if(file.isDirectory()){ //如果是文件夹
					num=num+getNum(file); //统计数量
				}
			}
		}
	return num; //返回值为数量
	}
}

5，每天下午5：00之前完成

```





```
NFFileCheckCommand.java


获得服务器目录路径 

FundFileConnectServiceImpl.java
	@Override
	public ChannelSftp FundFileConnect(FileJobParameter jobParameter) throws Exception {
	
	
FundFileConnect连接


String path=fileTransBean.getRemotePath();
System.out.println(path);



```





# SecureCRT与WinSCP

SecureCRT

SecureCRT是一款支持SSH（SSH1和SSH2）的终端仿真程序，简单地说是Windows下登录UNIX或Linux服务器主机的软件。





WinSCP是一个Windows环境下使用SSH的开源图形化SFTP客户端。同时支持SCP协议。它的主要功能就是在本地与远程计算机间安全的复制文件。

主要功能

- 图形用户界面
- 多语言
- 与 Windows 完美集成(拖拽, URL, 快捷方式)
- 支持所有常用文件操作
- 支持基于 SSH-1、SSH-2 的 SFTP 和 SCP 协议
- 支持批处理脚本和命令行方式
- 多种半自动、自动的目录同步方式
- 内置文本编辑器
- 支持 SSH 密码、键盘交互、公钥和 Kerberos(GSS) 验证
- 通过与 Pageant(PuTTY Agent)集成支持各种类型公钥验证
- 提供 Windows Explorer 与 Norton Commander 界面
- 可选地存储会话信息
- 可将设置存在配置文件中而非注册表中，适合在移动介质上操作

使用 WinSCP 可以连接到一台提供 SFTP (SSH File Transfer Protocol)或 SCP (Secure Copy Protocol)服务的 SSH (Secure Shell)服务器，通常是 UNIX 服务器。SFTP 包含于 SSH-2 包中，SCP 在 SSH-1 包中。两种协议都能运行在以后的 SSH 版本之上。WinSCP 同时支持 SSH-1 和 SSH-2。 但WinSCP不支持编码选择，也就是说，你在Windows下使用WinSCP连接一个Linux机器，因为Linux和Windows的默认编码不同，因此是无法访问上面的中文文件或者文件夹的（将看到乱码）。一种解决方法就是在打开winscp时登录中的 Advanced Options–Environment中将 “UTF-8 encoding for filenames”设为on.



NFFTY-SFTP



nfdelay南方基金快赎延迟发送
endpointCode: Nffund_Https
productProviderCode: NFFUND
jobIntervalUnit: hour

南方代销交易扩展文件对账com.mdiaf.recon.job.fund.nf.Consignment.NFFundTransExtDepositUploadCommand
endpointCode: NFFTY-SFTP
productProviderCode: NFFUND
jobIntervalUnit: day
mercId: 800004





PaymentProvider paymentProvider = paymentProviderOrmService.findOneById(Long.valueOf(param.get("providerId").toString()));
fundTradeRequest.setMercId(paymentProvider.getSObject().selectOne("PaymentParameter", ImmutableMap.of("ParamName", "mercId")).getString("ParamValue"));
fundTradeRequest.setVersion(paymentProvider.getSObject().selectOne("PaymentParameter", ImmutableMap.of("ParamName", "version")).getString("ParamValue"));


select * from paymentProvider;	//网易宝、实时支付、微信支付、南方基金、联泰、富聪平台。
select * from PaymentParameter;	//ParamName ParamValue: mercId 800008 南方基金商户号; mercId 800011 联泰商户号;800004腾元商户号
select * from IsgEndpointOut;	//NFFLT-SFTP

设置--系统API管理--交易目标端口：Endpoint Name: NFFLT-SFTP， 121.35.255.69 	User ID: nf_test Password: test1
(其实这些信息 在表IsgEndpointOut中可以查到。





FundFileTransProcessServiceImpl.java

```
public void fundFileUpload(FileJobParameter jobParameter) throws Exception {
		log.info(jobParameter.getProductProviderCode()+"数据处理开始执行！");
		long start = System.currentTimeMillis();
		// 0. 配置初始化(包括文件配置、通信配置等).
		InsuranceFileTransBean fileTransBean = fundFileJobGeneralService.createFileTransBean(jobParameter);
		// 1. 获取数据
		InsuranceFileDataBean fileDataBean  = fundFileJobGeneralService.getInsuranceFileData(fileTransBean,jobParameter.getProductProviderCode());
		// 2. 生成文件
		fundJobGeneralService.createAndWriteFile(fileTransBean, jobParameter,fileDataBean);
		// 3. 创建SFTP连接
		ChannelSftp channelSftp = fundJobGeneralService.createChannelSftp(fileTransBean);
		if(channelSftp.isConnected()){
			System.out.println("hello");
		}
		// 4. 上载新契约交易文件
		fundJobGeneralService.uploadFile(channelSftp, fileTransBean, jobParameter);
		// 5. 修改文件名
		fundJobGeneralService.renameFileToBak(fileTransBean, jobParameter);
		log.info(jobParameter.getProductProviderCode()+" - 批量文件上传成功,耗时"+(System.currentTimeMillis()-start)+"ms!");

		
	}
	
```

上面在uploadFile()中，sftp链接关闭了。

 



```

		String path=fileTransBean.getRemotePath();
		System.out.println(path);
		if(channelSftp.isConnected()){
			System.out.println("hello2");
		}
		
		Vector fileList; 
		fileList=channelSftp.ls(path);
//		List<String> fileNameList = new ArrayList<String>(); 
		Iterator it = fileList.iterator(); 
		System.out.println(fileList.toString());
```


