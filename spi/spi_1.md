

# 20170720

昨天装软件
1，安装jdk，配置对应的环境变量。
2，安装git和sourcetree（在sourcetree中指定git.exe路径）
3，gitlab地址[http://172.16.1.101/users/sign_in](http://172.16.1.101/users/sign_in)
对应项目路径
4，在Source Tree中拉取项目
安装STS
修改STS的启动参数（STS.init）：
-Xms2000m
-Xmx2000m
-XX:MaxPermSize=256m

STS.init:
(eclipse.ini是一个文本文件，其内容相当于在Eclipse运行时添加到 Eclipse.exe之后的命令行参数。)
其格式要求：
所有的选项及其相关的参数必须在单独的一行之内;
所有在-vmargs之后的参数将会被传输给JVM，所有如果所有对Eclipse 设置的参数必须写在-vmargs之前（就如同你在命令行上使用这些参数一样）
默认情况下，eclipse.ini的内容如下：
-showsplash
org.eclipse.platform
--launcher.XXMaxPermSize
256m
-vmargs
-Xms40m
-Xmx256m
上面的配置表示堆空间初始大小为40M，最大为256M，PermGen最大为256M。

(我的STS.ini的配置：
-startup
plugins/org.eclipse.equinox.launcher_1.3.100.v20150511-1540.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.300.v20150602-1417
-product
org.springsource.sts.ide
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
256M
-vmargs
-Dosgi.requiredJavaVersion=1.6
-Xms2000m
-Xmx2000m
-XX:MaxPermSize=256m
-Xverify:none
-Dorg.eclipse.swt.browser.IEVersion=10001
)

Eclipse配置Tomcat服务器
- 打开Eclipse，单击“window”菜单，选择下方的“Preferences”：
- 找到Server下方的Runtime Environment，单击右方的Add按钮：
- 选择已经成功安装的Tomcat版本，单击Next:
- 设置Tomcat的安装目录，设置完成后，单击OK即可完成设置！
  Tomcat参数配置：
  启动时间配置
  Vm参数配置，-XX:MaxPermSize=256m -Xmx1500m
  URI Encoding: UTF-8
  <Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>



##渤海

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



## 南方货基

写一个job 检测南方基金 余额查询接口通不通.
FundTransAdapter.shareBalanceQuery()余额查询接口
nffundAdapter 南方基金路由
WithdrawDelayCommand 
feature/jira/201708/FC-386
路由Adapter是什么意思
周四发 所以 尽快搞清楚

问题：
南方货基：
http请求 200（我们的请求时？）
FundTransAdapter.shareBalanceQuery()余额查询接口 
public ShareBalanceQueryResponse shareBalanceQuery(ShareBalanceQueryRequest shareBalanceQueryRequest) throws Exception;
有很多实现，
根据返回的ShareBalanceQueryResponse的值判断余额查询通不通。
public  FundTransAdapter  nffundAdapter (){}



## 仿照的例子：nfdelay南方基金快赎延迟发送
com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand
WithdrawDelayCommand
nfdelay南方基金快赎延迟发送
@Component
public class WithdrawDelayCommand extends AbstractUploadReconCommand {

网易金融业务管理系统（http://172.16.1.131:8080/aiaf/ ）
设置--批处理管理--Job/Schedules--name 查询--	JobParameters()
http://localhost:8080/aiaf/BmfAggrEditor/BatchModule?bmfAggrId=313522
nfdelay南方基金快赎延迟发送 ：run job。
LastSuccessJobKey: 2017072402
Job Code: com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand



```
@Component("nffundFundTransAdapter")
public class NffundFundTransAdapter implements FundTransAdapter {


@Override
public FundTradeResponse fundTrade(FundTradeRequest fundTradeRequest) throws Exception {
	FundTradeResponse response = null;
	try {
		response = (FundTradeResponse) nFFundTradeHandler.handle(fundTradeRequest);
		return response;
	} finally {
		publishEvent(fundTradeRequest, response, FundInterfaceEnum.NFFUND_TRADE.getCode());
	}
}
```















## FundAdapterCheckCommand 

com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand

    @Autowired
    private FundJobGeneralService fundJobGeneralService;
    
    @Autowired
    @Qualifier("nFFundWithdrawDelayServiceImpl")
    private FundRealTimeTransService fundRealTimeTransService;
fundRealTimeTransService.realTimeTransProcess(jobParameter); 这个方法是 nFFundWithdrawDelayServiceImpl的抽象类的。
public abstract class AbstractFundRealTimeTransService implements FundRealTimeTransService {
public class NFFundWithdrawDelayServiceImpl extends AbstractFundRealTimeTransService{

public interface FundRealTimeTransService {

实现类调用抽象类的方法，




FundTransAdapter：（open type hierarchy F4） 
@Component("nffundAdapter"		//这里nffundAdapter 是 FundTransAdapterCategory 的别名，当后面应用时就可以 @Qualifier("nffundAdapter")
public class FundTransAdapterCategory implements FundTransAdapter {

private FundTransAdapter getAdapter(String productProviderCode) {

```
@Override
public ShareBalanceQueryResponse shareBalanceQuery(ShareBalanceQueryRequest shareBalanceQueryRequest) throws Exception {
return getAdapter(shareBalanceQueryRequest.getProductProviderCode()).shareBalanceQuery(shareBalanceQueryRequest);
	}
```

@Component("nffundFundTransAdapter")
public class NffundFundTransAdapter implements FundTransAdapter {
```
@Override
public ShareBalanceQueryResponse shareBalanceQuery(ShareBalanceQueryRequest shareBalanceQueryRequest) throws Exception {
        return (ShareBalanceQueryResponse)  nFShareBalanceQueryMessageHandler.handle(shareBalanceQueryRequest);
	}
```



@Component
public class FundAdapterCheckCommand extends AbstractUploadReconCommand {
public abstract class AbstractUploadReconCommand implements BafJobCommand {
```
package com.mdiaf.batch.service;
import java.util.List;
import org.quartz.JobExecutionContext;
import com.mdiaf.bmf.SObject;
public interface BafJobCommand {
	String getJobInstKey(Object jobParameters, SObject jobId) throws Exception;
	void execute(JobExecutionContext context) throws Exception;
	public List<String> getMissedJobs(Long jobId);
}
```





```
@Component("nffundFundTransAdapter")
public class NffundFundTransAdapter implements FundTransAdapter {



@Override
public ShareBalanceQueryResponse shareBalanceQuery(ShareBalanceQueryRequest shareBalanceQueryRequest) throws Exception {
	return (ShareBalanceQueryResponse) nFShareBalanceQueryMessageHandler.handle(shareBalanceQueryRequest);
}
```














UAT环境：
uat1 http://172.16.1.131:8080/aiaf/index?redirecting=false
uat2，http://172.16.1.127:8080/aiaf/index?redirecting=false
ust3，http://172.16.1.128:8080/aiaf/index?redirecting=false
ust4，http://172.16.1.1129:8080/aiaf/index?redirecting=false
h5,	http://uat2.nfs.org/h5/Dashboard/Dashboard.html
h5,	http://172.16.1.131/h5/Dashboard/Dashboard.html

接口：
DOC里的接口

实时

##Eclipse中快速输入代码的自动补全是按enter而不是tab。
alt+/：自动找到相关语句。
ctr+e：转换编辑器
ctr+O：outline
ctr+shift+R：快速打开资源


##eclipse  ctrl+左键 查看源代码 提示找不到源时

在eclipse进行java编程时，查看类源代码，这时ctrl+鼠标左键是个很常用的操作，但有时发现实现不了，经常显示找不到源码。
打开
点击连接源代码----选择”External location“----在此对话框下，选择”External location“---找到路径为安装java JDK时的路径，关键是在此路径下，找到src.zip,就行了。



#20170721


##受工作交接


修改：众诚精确报价---投保人被保人信息
所在分支
DOC：Develop分支
NFS：feature/jira/FC-383

ZcQuotePriceRequestConvert类


```
一、众诚精确报价-投保人、被保人信息来源更改
原来两者默认为车主信息，现在更改为由数据库查询得来，修该ZcQuotePriceRequestConvert类，代码如下：

// 投保人
List<PolicyHolder> policyHolderList = createPolicyHolderInfo(agreement);
// 被保人
List<Insured> insureds = createInsuredInfo(agreement);

private List<PolicyHolder> createPolicyHolderInfo(Agreement agreement) throws InsuranceException {
		List<PolicyHolder> policyHolderList = new ArrayList<PolicyHolder>();
		PolicyHolder policyHolder = new PolicyHolder();
		List<ClientAgreementRole> phClientAgreementRoleList = clientAgreementRoleOrmService.findAllByClientId_AgreementId_RoleType(agreement.getClientId(), agreement.getOid(), InsuranceConstants.PolicyHolder);
		if(CollectionUtils.isNotEmpty(phClientAgreementRoleList)){
			policyHolder.setPolicyHolder(phClientAgreementRoleList.get(0).getInsuredName());
			policyHolderList.add(policyHolder);
		}else{
			throw new InsuranceException("众诚车险报价，未查询到投保人信息！");
		}
		return policyHolderList;
	}


private List<Insured> createInsuredInfo(Agreement agreement) throws InsuranceException {
		List<Insured> insureds = new ArrayList<Insured>();
		Insured insured = new Insured();
		List<ClientAgreementRole> insuredClientAgreementRoleList=clientAgreementRoleOrmService.findAllByClientId_AgreementId_RoleType(agreement.getClientId(), agreement.getOid(), InsuranceConstants.Insured);
		if(CollectionUtils.isNotEmpty(insuredClientAgreementRoleList)){
			insured.setInsuredName(insuredClientAgreementRoleList.get(0).getInsuredName());
			insured.setHasMinor(ZcConstant.HASMINOR); // 默认无未成年子女
			insured.setBirthday(insuredClientAgreementRoleList.get(0).getBirthday());
			insured.setGender(insuredClientAgreementRoleList.get(0).getSex());
			insureds.add(insured);
		}else{
			throw new InsuranceException("众诚车险报价，未查询到被保人信息！");
		}
		
		return insureds;
	}

二、亚泰风险测评结果同步
LtfundFundTransAdapter类中syncRiskQuestionnaire方法：
@Override
	public RiskQuestionnaireResponse syncRiskQuestionnaire(RiskQuestionnaireRequest riskQuestionnaireRequest) throws Exception {
log.info("联泰风险测评问卷答案同步，farms请求报文,{}",JsonUtils.marshalFormat(riskQuestionnaireRequest));
		
		//拼装参数
fundSupportService.getSpiTemporaryData(riskQuestionnaireRequest, bmfManager.getLtEnvironmentVariate());
		//请求转换
LtRiskQuestionaireRequest request = ltRiskQuestionaireQuestionRequestConverter.convert(riskQuestionnaireRequest);
		//计算sign
LTRequestMessage ltRequestMessage = LtFundHandler.transBean2XML(getRequestBody(request),riskQuestionnaireRequest,riskQuestionnaireRequest.getApplyTimeStr(),LTBusinessCodeAndUrlEnum.SYNCRISKQUESTIONNAIRE.getCode());
		//接口调用
LTRiskQuestionaireResponse response = LtFundHandler.handle(riskQuestionnaireRequest, ltRequestMessage, LTRiskQuestionaireResponse.class);
		
RiskQuestionnaireResponse riskQuestionnaireResponse = ltRiskQuestionaireResponseConverter.convert(response);
		 
		log.info("联泰风险测评问卷答案同步，farms返回报文,{}",JsonUtils.marshalFormat(riskQuestionnaireResponse));
		//返回
		return riskQuestionnaireResponse;
				
	}

```























## 判断一个对象是什么类型的方法

任意给一个变量,有没有办法判断它是数据类型还是对象类型?具体是什么类型?

```
java里对基本数据类型应该是没有直接判断方法的，但是可以自己利用函数重载实现： 
public   static   String   typeOf(boolean   var){   
          return   "boolean   ";   
  }   
  public   static   String   typeOf(char   var){   
          return   "char   ";   
  }   
  public   static   String   typeOf(int   var){   
          return   "int";   
  }   
反正一共也只有几种类型，全部写完好了。 
对于对象类型： 
public   static   String   typeOf(Object   var){   
          return   var.getClass().toString();   
  }  
```



## git报错 error: cannot stat ‘file’: Permission denied

切换分支时报错：
　　error: cannot stat ‘file’: Permission denied
解决方法：退出编辑器、浏览器、资源管理器等，然后再切换就可以了。



# 20170724

容器
bean
spring bean
java bean
工厂模式、工厂方法
容器
设计模式





## org.springframework.stereotype

- [Component]
- [Controller]
- [Repository]
- [Service]

@Repository、@Service、@Controller 和 @Component 将类标识为Bean

@Repository注解便属于最先引入的一批，它用于将数据访问层 (DAO 层 ) 的类标识为 Spring Bean。具体只需将该注解标注在 DAO类上即可。同时，为了让 Spring 能够扫描类路径中的类并识别出 @Repository 注解，需要在 XML 配置文件中启用Bean 的自动扫描功能，这可以通过<context:component-scan/>实现。

如此，我们就不再需要在 XML 中显式使用 <bean/> 进行Bean 的配置。Spring 在容器初始化时将自动扫描 base-package 指定的包及其子包下的所有 class文件，所有标注了 @Repository 的类都将被注册为 Spring Bean。

Spring 2.5 在 @Repository的基础上增加了功能类似的额外三个注解：@Component、@Service、@Constroller，它们分别用于软件系统的不同层次：

- @Component 是一个泛化的概念，仅仅表示一个组件 (Bean) ，可以作用在任何层次。
- @Service 通常作用在业务层，但是目前该功能与 @Component 相同。
- @Constroller 通常作用在控制层，但是目前该功能与 @Component 相同。

事实上这几个注解并没有任何功能上的区别，你可以把这些当做是分类标签，目的是为了让你的代码可读性更强

```
| Annotation | Meaning                                             |
+------------+-----------------------------------------------------+
| @Component | generic stereotype for any Spring-managed component |
| @Repository| stereotype for persistence layer                    |
| @Service   | stereotype for service layer                        |
| @Controller| stereotype for presentation layer (spring-mvc)      |
```







## JIRA

JIRA是Atlassian公司出品的项目与事务跟踪工具，被广泛应用于缺陷跟踪、客户服务、需求收集、流程审批、任务跟踪、项目跟踪和敏捷管理等工作领域。



# 20170725



JavaDoc



shareBalanceQuery





​	WITHDRAW_DEPYL("WITHDRAW_DEPYL","WITHDRAW_DEPYL","快赎延迟发送"),

这个对应于word文档的那一个

我的对应

eclipse项目上出现 > 符号,表示 此項目內包含資源版本改變未同步的文件。 







# 20170727

java与python关系

java用jar包

python通过pip install package，之后通过import package完成

spring框架与python对应的框架的话： 



spring框架

各个包提供了各个接口

一个工作空间 一个配置环境 validation等



## clean作用

eclipse为了提高效率，并不是每次启动项目都会检查插件，通过clean就是强制eclipse去检查已安装插件。

我们都知道.[Java](http://lib.csdn.net/base/java)文件是通过编译成.class文件运行的，而clean后会删除已经编译生成的.class文件并重新部署项目。

总起来将就是强制检查已安装插件，清除以前编译的信息，重新部署项目。











warning---error

java--compiler--errors/warnings

## eclipse部署上Tomcat后的clean和publish功能

**publish**:是将你的web程序发布到tomcat服务器上，这样通过浏览器就可以访问你的程序。
**clean**：是指原先编译到tomcat服务器上的程序，先清除掉，然后再重新编译。

publish的作用就是发布。然后浏览效果。
clean的使用，一般publish提示有错误或更改没效果，clean一下就可以清除之前的编译。
如：我建了一个Hello.java的类。然后我publish，现在我把这个类删除了，我要clean一下，才能清除这个.class文件.

安装了JDK1.8之后，eclipse自动设置为了JDK1.8 。 手动再添加1.7





## 调试







```
 @Override
    public void execute(JobExecutionContext context) throws Exception {
        logger.info("南方基金快赎延后发送begin");
        JobDataMap dataMap = context.getMergedJobDataMap();
        String jobParameters = dataMap.getString("jobParameters");
        if(StringUtils.isEmpty(jobParameters)){
            throw new Exception("lastSuccessDate有误，请确认！");
        }
        logger.info("JobParameters: " + jobParameters);
        dataMap.put("jobParameters", getStartEndInstKey(jobParameters));
        
        RealTimeJobParameter jobParameter = fundJobGeneralService.createRealTimeJobParameter(dataMap, NFFileCategoryAndNameEnum.WITHDRAW_DEPYL.getCategory());
        fundRealTimeTransService.realTimeTransProcess(jobParameter);
    }
```


context--jobDataMap--Map:
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=421873224, triggerMode=Manual, jobInstanceOid=423005784, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand, jobParameters=2017073002, lockMode=, transAcct=8000081511051024}

JobDataMap dataMap = context.getMergedJobDataMap();
public JobDataMap getMergedJobDataMap() {
    return jobDataMap;
}
String jobParameters = dataMap.getString("jobParameters");
dataMap--map:
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=421873224, triggerMode=Manual, jobInstanceOid=423005784, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand, jobParameters=2017073002, lockMode=, transAcct=8000081511051024}

dataMap.put("jobParameters", getStartEndInstKey(jobParameters));
dataMap
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=421873224, triggerMode=Manual, jobInstanceOid=423005784, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand, jobParameters=2017072902-2017073002, lockMode=, transAcct=8000081511051024}



网页端配置：
JobParameters（jobIntervalUnitP: hour, endpointCode: Nffund_Https, productProviderCode: NFFUND）

**this**---WithdrawDelayCommand(id=9913)
com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand@11d09b49
com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand@6a8178dd
com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand@6a8178dd

**context**：---JobExecutionContextImpl(id=24599)
JobExecutionContext: 
trigger: 'DEFAULT.MT_2b5xnwvcudt8o 
job: DEFAULT.nfdelay南方基金快赎延迟发送 
fireTime: 'Tue Aug 01 10:33:48 CST 2017 
scheduledFireTime: Tue Aug 01 10:33:48 CST 2017 
previousFireTime: 'null nextFireTime: null 
isRecovering: false 
refireCount: 0
context---jobDataMap--org.quartz.JobDataMap@5332ab80: Map
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=148641112, triggerMode=Manual, jobInstanceOid=423005820, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand, jobParameters=2017070202, lockMode=}

**dataMap**
org.quartz.JobDataMap@5332ab80
Map:
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=148641112, triggerMode=Manual, jobInstanceOid=423005832, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand, jobParameters=2017070202, lockMode=}

**jobParameters**
2017070202

dataMap.put("jobParameters", getStartEndInstKey(jobParameters));
getStartEndInstKey(jobParameters)
public String getStartEndInstKey(String  jobEndTime){
      return convertDate(jobEndTime,-1)+"-"+ jobEndTime;//把jobParameters减去1天，
}
dataMap
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=148641112, triggerMode=Manual, jobInstanceOid=423005832, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand, jobParameters=2017070102-2017070202, lockMode=}


RealTimeJobParameter jobParameter = fundJobGeneralService.createRealTimeJobParameter(dataMap, NFFileCategoryAndNameEnum.WITHDRAW_DEPYL.getCategory());
fundRealTimeTransService.realTimeTransProcess(jobParameter);

public RealTimeJobParameter createRealTimeJobParameter(JobDataMap dataMap,String businessType) throws Exception {
Long jobId = dataMap.getLong("jobId");
Long jobInstanceOid = dataMap.getLong("jobInstanceOid");
String jobInstKey = dataMap.getString("jobParameters");
String productProviderCode = reconSupportService.getRunJobParameterById(jobId, InuranceJobParameterEnum.PRODUCTPROVIDERCODE.getCode(), "");	//这里 productProviderCode=NFFUND

public String getRunJobParameterById(Long jobId, String parameterName, String defaultValue) {
		String jobParameterValue = null;
		SObject jobSObject = reconSupportDao.findSObject("BafJob", jobId);//tableName,oid
		
		BmfTable table = this.getBatchTable("BafJobParameter");
		BmfAggrQuery query = new BmfAggrQuery();
		query.setTargetBmfTable(table);
		query.setParentId(jobSObject.getOid());
		query.addQueryParam("Name", parameterName);

		List<SObject> jobParameterList = bmfOrmAggrManager.findSObject(query);
		if (CollectionUtils.isNotEmpty(jobParameterList)) {
			SObject jobParameter = jobParameterList.get(0);
			jobParameterValue = jobParameter.getString("Value");
		}

		if (StringUtils.isEmpty(jobParameterValue)) {
			jobParameterValue = defaultValue;
		}
		return jobParameterValue;
	}

在 “nfdelay南方基金快赎延迟发送” 参数配置页面配置的信息 全部被放到了BafJob表中了。	
根据jobId查询jobSobject  得到“nfdelay南方基金快赎延迟发送”
最终得到String productProviderCode=“NFFUND”









@Repository
public class ReconSupportDaoImpl implements ReconSupportDao {
@Override
	public SObject findSObject(String tableName, Long oid) {
		OrmUtilities.modifyBegin();
		SObject sobject = bmfOrmAggrManager.findOne(tableName, oid);
		OrmUtilities.modifyEnd();
		return sobject;
	}




JobExecutionContext: 
trigger: 'DEFAULT.MT_3shfphgl6um1i 
job: DEFAULT.nfdelay南方基金快赎延迟发送 
fireTime: 'Mon Jul 31 15:35:39 CST 2017 
scheduledFireTime: Mon Jul 31 15:35:39 CST 2017 
previousFireTime: 'null 
nextFireTime: null 
isRecovering: false 
refireCount: 0
context--jobDataMap--map:
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=148641112, triggerMode=Manual, jobInstanceOid=423005800, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand, jobParameters=2017073102, lockMode=}
JobDataMap dataMap = context.getMergedJobDataMap();
dataMap--map:
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=148641112, triggerMode=Manual, jobInstanceOid=423005800, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand, jobParameters=2017073102, lockMode=}
String jobParameters = dataMap.getString("jobParameters");
jobParameters: 2017073102
dataMap.put("jobParameters", getStartEndInstKey(jobParameters));
dataMap--map:
{endpointCode=Nffund_Https, jobType=Java Bean, jobIntervalUnit=hour, jobId=148641112, triggerMode=Manual, jobInstanceOid=423005800, productProviderCode=NFFUND, springBatchJob=, jobCode=com.mdiaf.recon.job.fund.nf.WithdrawDelayCommand, jobParameters=2017073002-2017073102, lockMode=}

jobId: 148641112
jobInstanceOid: 423005800
jobInstKey: 2017073002-2017073102
secretkeyType: null
secretkeyParam: null
contentFileName: null
targetFileName: null
targetEndPointCode: null
productProviderCode: NFFUND
endpointCode: Nffund_Https
productCode: null
transAcct: null 

获取环境变量：
IsgEndpointOut endpointOutSObject = reconSupportService.getIsgEndpointOut(endpointCode);
String url = endpointOutSObject.getURL();
Integer timeout = endpointOutSObject.getTimeout();
String password = endpointOutSObject.getSignKey();//腾元取值 password , 联泰取值是instid

endpointOutSObject: Nffund_Https
url: https://121.35.255.69:447/kdwis/fsServiceServlet
timeout: 60
password: 1234567890ABCDEFG

jobIntervalUnit： hour
//----公私密钥-----
ProductProviderSecretkey productProviderSecretkey = 	reconSupportService.getProductProviderSecretKeyByproductProviderCode(productProviderCode,secretkeyType,secretkeyParam);
productProviderSecretkey： com.sun.jdi.InvocationException occurred invoking method.





**dataMap：**
org.quartz.JobDataMap@445d2bc0
**jobParameters:**
2017072702
**jobParameter:**
FileJobParameter 
[
productProviderCode=NFFUND, 
endpointCode=Nffund_Https, 
jobInstKey=2017072602-2017072702, 
jobIntervalUnit=hour, 
jobIntervalValue=null, 
jobInstanceOid=422590052, 
businessType=WITHDRAW_DEPYL, 
mercId=null, 
creater=null, 
receiver=null, 
fileProductProviderCode=null, 
contentFileType=null, 
contentFileName=null, 
timeStampVariable=null, 
sendPhones=null, 
productCode=null, 
encode=null, 
isVerification=null, 
fileType=null, 
verificationFileType=null, 
ormReturnFlag=null, 
mobile=null
]




package com.mdiaf.recon.fund.service;
public interface FundJobGeneralService {

package com.mdiaf.recon.fund.service.impl;
@Service
public class FundJobGeneralServiceImpl implements FundJobGeneralService{





0 5 2,3 * * ?
2017/8/1 2:05:00
2017/8/1 3:05:00
2017/8/2 2:05:00
2017/8/2 3:05:00
0 0/30 2,3 * * ? 
2017/8/1 2:00:00
2017/8/1 2:30:00
2017/8/1 3:00:00
2017/8/1 3:30:00
2017/8/2 2:00:00






```
@Override 
	public void realTimeTransProcess(RealTimeJobParameter jobParameter) throws Exception {
		// 0. 配置初始化(包括文件配置、通信配置等).
		InsuranceFileTransBean fileTransBean = fundFileProcessStrategy.createFileTransBean(jobParameter);
		// 1. 获取数据
		InsuranceFileDataBean fileDataBean  = this.createFileDataBean(jobParameter, fileTransBean);
		processInvestData(jobParameter,fileDataBean,fileTransBean);
	}
```
jobParameter
fileTransBean:
com.mdiaf.recon.bean.insurance.InsuranceFileTransBean@4beb920f
fileDataBean:
com.mdiaf.recon.bean.insurance.InsuranceFileDataBean@61640d84



**this**
com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand@715e38de
**context**：
JobExecutionContext: 
trigger: 'DEFAULT.MT_4gdgqm7pl46nb 
job: DEFAULT.nf南方基金余额查询接口校验 
fireTime: 'Thu Jul 27 16:16:00 CST 2017 
scheduledFireTime: Thu Jul 27 16:16:00 CST 2017 
previousFireTime: 'null 
nextFireTime: null 
isRecovering: false 
refireCount: 0
**dataMap：**
org.quartz.JobDataMap@b4cc0707
**jobParameters:**
2017072602
**jobParameter:**
FileJobParameter 
[
productProviderCode=NFFUND, 
endpointCode=Nffund_Https, 
jobInstKey=2017072502-2017072602, 
jobIntervalUnit=hour, 
jobIntervalValue=null, 
jobInstanceOid=422590060, 
businessType=ADAPTER_CHECK, 
mercId=null, 
creater=null, 
receiver=null, 
fileProductProviderCode=null, 
contentFileType=null, 
contentFileName=null, 
timeStampVariable=null, 
sendPhones=null, 
productCode=null, 
encode=null, 
isVerification=null, 
fileType=null, 
verificationFileType=null, 
ormReturnFlag=null, 
mobile=null
]


web.xml 而不是 server.xml
原因是因为在tomcat重启的时候，之前的tomcat的线程还没有完全关闭，最新启动tomcat就会报这个异常，只要把tomcat的server.xml 中的reloadable="true" 改成false就OK









listary问题 导致了 no more handles





```
try {
				for (Map<String, Object> params : list) {
					//检查参数
					checkData(params);
					ShareBalanceQueryRequest shareBalanceQueryRequest = convertShareBalanceQueryRequest(params);
					ShareBalanceQueryResponse shareBalanceQueryResponse = fundTransAdapter.shareBalanceQuery(shareBalanceQueryRequest);
					log.info("余额查询校验结果:{}", JsonUtils.marshal(shareBalanceQueryResponse));
					//应答码
					if (StringUtils.equals(shareBalanceQueryResponse.getRetCode(), TransSuccessStatus.SUCCESS.getValue())) {
						//成功后通知Farms
						paymentEventApiService.retryPaymentRequest(Long.valueOf(params.get("paymentRequestId").toString()), Boolean.FALSE);
						log.info("延迟快赎发送成功,调用Farms接口更新状态,PaymentRequestId = {}", params.get("paymentRequestId").toString());
					}else{
						throw new FundDomainException("南方基金接口异常,请立即确认！");
					}
				}
			} catch (Exception e) {
				log.error(e.getMessage());
				throw e;
			}
```







WithdrawDelayCommand
每天晚上两点-三点  南方基金快赎 关闭， 我们通过快赎延迟发送 机制在之后延迟发送，第二天发送 正常。





后面的参数自己设一下

还是要用到前边的 

看一下 word文档



# 20170728

## maven





## @Service @Qualifier@Autowired

```
package org.springframework.beans.factory.annotation;
import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Inherited;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
/**
 * This annotation may be used on a field or parameter as a qualifier for
 * candidate beans when autowiring. It may also be used to annotate other
 * custom annotations that can then in turn be used as qualifiers.
 * @author Mark Fisher
 * @author Juergen Hoeller
 * @since 2.5
 * @see Autowired
 */
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @interface Qualifier {
	String value() default "";
}
```



```
package org.springframework.stereotype;
import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
/**
 * Indicates that an annotated class is a "Service", originally defined by Domain-Driven
 * Design (Evans, 2003) as "an operation offered as an interface that stands alone in the
 * model, with no encapsulated state."
 * <p>May also indicate that a class is a "Business Service Facade" (in the Core J2EE
 * patterns sense), or something similar. This annotation is a general-purpose stereotype
 * and individual teams may narrow their semantics and use as appropriate.
 * <p>This annotation serves as a specialization of {@link Component @Component},
 * allowing for implementation classes to be autodetected through classpath scanning.
 * @author Juergen Hoeller
 * @since 2.5
 * @see Component
 * @see Repository
 */
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Service {
	/**
	 * The value may indicate a suggestion for a logical component name,
	 * to be turned into a Spring bean in case of an autodetected component.
	 * @return the suggested component name, if any
	 */
	String value() default "";
}
```

```
package org.springframework.beans.factory.annotation;
import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
/**
 * Marks a constructor, field, setter method or config method as to be
 * autowired by Spring's dependency injection facilities.
 * <p>Only one constructor (at max) of any given bean class may carry this
 * annotation, indicating the constructor to autowire when used as a Spring
 * bean. Such a constructor does not have to be public.
 * <p>Fields are injected right after construction of a bean, before any
 * config methods are invoked. Such a config field does not have to be public.
 * <p>Config methods may have an arbitrary name and any number of arguments;
 * each of those arguments will be autowired with a matching bean in the
 * Spring container. Bean property setter methods are effectively just
 * a special case of such a general config method. Such config methods
 * do not have to be public.
 * <p>In the case of multiple argument methods, the 'required' parameter is
 * applicable for all arguments.
 * <p>In case of a {@link java.util.Collection} or {@link java.util.Map}
 * dependency type, the container will autowire all beans matching the
 * declared value type. In case of a Map, the keys must be declared as
 * type String and will be resolved to the corresponding bean names.
 * <p>Note that actual injection is performed through a
 * {@link org.springframework.beans.factory.config.BeanPostProcessor
 * BeanPostProcessor} which in turn means that you <em>cannot</em>
 * use {@code @Autowired} to inject references into
 * {@link org.springframework.beans.factory.config.BeanPostProcessor
 * BeanPostProcessor} or
 * {@link org.springframework.beans.factory.config.BeanFactoryPostProcessor BeanFactoryPostProcessor}
 * types. Please consult the javadoc for the {@link AutowiredAnnotationBeanPostProcessor}
 * class (which, by default, checks for the presence of this annotation).
 * @author Juergen Hoeller
 * @author Mark Fisher
 * @since 2.5
 * @see AutowiredAnnotationBeanPostProcessor
 * @see Qualifier
 * @see Value
 */
@Target({ElementType.CONSTRUCTOR, ElementType.FIELD, ElementType.METHOD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {
	/**
	 * Declares whether the annotated dependency is required.
	 * <p>Defaults to {@code true}.
	 */
	boolean required() default true;
}
```




流程：先看大概流程，干了一件什么事。
看返回类型


拦截
那个时间段内的交易查询出来，重新发送

command


放开断点 之后 调试直接完成。



NFFileCategoryAndNameEnum.WITHDRAW_DEPYL.getCategory()
枚举类
```
package com.shidexiao.test;
/**
 * 枚举测试类
 * 
 * @author <a href="mailto:hemingwang0902@126.com">何明旺</a>
 */
public enum Enum_Test {
	MON(1), TUE(2), WED(3), THU(4), FRI(5), SAT(6) {
        @Override
        public boolean isRest() {
            return true;
        }
    },
    SUN(0) {
        @Override
        public boolean isRest() {
            return true;
        }
    };
    private int value;
    private Enum_Test(int value) {
        this.value = value;
    }
    public int getValue() {
        return value;
    }
    public boolean isRest() {
        return false;
    }
}

package com.shidexiao.test;
public class Test_enum {
	 public static void main(String[] args) {
	        System.out.println("EnumTest.FRI 的 value = " + Enum_Test.FRI.getValue());
	    }
}
```





# 20170731 


##Java 修饰符

###访问修饰符
Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java支持4种不同的访问权限。
默认的，也称为 default，在同一包内可见，不使用任何修饰符。
私有的，以 private 修饰符指定，在同一类内可见。
共有的，以 public 修饰符指定，对所有类可见。
受保护的，以 protected 修饰符指定，对同一包内的类和所有子类可见。
###非访问修饰符
为了实现一些其他的功能，Java 也提供了许多非访问修饰符。
static 修饰符，用来创建类方法和类变量。
final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。
abstract 修饰符，用来创建抽象类和抽象方法。
synchronized 和 volatile 修饰符，主要用于线程的编程。

static 修饰符，用来创建类方法和类变量。
对类变量和方法的访问可以直接使用 classname.variablename 和classname.methodname 的方式访问。



##常用注解

org.springframework.stereotype
Annotation Types
Component
Controller
Repository
Service

java.lang.annotation
Interfaces：Annotation
Enums：ElementType	RetentionPolicy
Exceptions：AnnotationTypeMismatchException IncompleteAnnotationException
Errors：AnnotationFormatError
Annotation Types：Documented Inherited Retention Target



nf南方基金余额查询接口校验   改名为  nf南方接口健康性检查


业务运营DMSManagement---业务伙伴---南方基金管理有限公司---


#核心代码
FundRealTimeTransService
  |----AbsstractBankRealTimeTransService

  |----AbsstractFundRealTimeTransService
	 |----NFFundShareBalanceCheckServiceImpl
	 |----NFFundWithdrawDelayServiceImpl
	 |----LTDepositFileDownloadServiceImpl
	 |----LTDepositFileDownloadServiceImpl


##问题
package com.mdiaf.recon.bean.insurance;
public class FileJobParameter {
这里边的变量是可以自己添加的吗？


package com.mdiaf.recon.bean.insurance;
public class RealTimeJobParameter extends FileJobParameter{


package com.mdiaf.recon.fund.service.impl;
@Service
public class FundJobGeneralServiceImpl implements FundJobGeneralService{
@Override
public RealTimeJobParameter createRealTimeJobParameter(JobDataMap dataMap,String businessType) throws Exception {
		RealTimeJobParameter jobParameter = new RealTimeJobParameter();
		.........
		return jobParameter;


​		
sftp：Secure File Transfer Protocol，安全文件传送协议。可以为传输文件提供一种安全的网络的加密方法。
sftp 与 ftp 有着几乎一样的语法和功能。SFTP 为 SSH的其中一部分，是一种传输档案至 Blogger 伺服器的安全方式。

FTP 是File Transfer Protocol（文件传输协议）的英文简称，而中文简称为“文传协议”。
ssh：Secure Shell （安全外壳协议），SSH 为建立在应用层基础上的安全协议。




##打印机不能打印问题
安装完之后。设备和打印机--打印机属性--端口--配置端口--打印机名或打印机地址172.16.1.33

#maven本地仓库.m2文件夹




##查看日志tail等 命令行使用小技巧
如何让Windows的cmd或PowerShell正常显示UTF-8字符
powershell与cmd
首先help一下，发现chcp命令可以改变代码页。（〉help）
敲下chcp 65001（936是gbk 65001utf-8）

帮助：help command 或者 command /？




7675760	26672		0		26672		104317	104316	2015-08-06 08:39:43	3000-01-01 00:00:00	1	2015-08-06 08:39:43	2015-08-06 08:55:34	18599	18599		NFF	南方基金						Active


version 1.0
mercId 800008
fundcode 000719


#20170802

server configuration: arguments 中添加-Dspring.profiles.active="dev,JobTriggerAndExecutor"


http://172.16.1.131:8080/aiaf/BmfAggrEditor/AdministrationModule?bmfAggrId=8773
config params
host
mode

