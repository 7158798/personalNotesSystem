

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


#20170803

1分钟---7分钟---1分钟---5分钟



spi.log 与 job.log  只保存当天的数据
spi.log 

若LastSuccessJobKey:与LastSuccessDate:相同，则测试 进行不下去， 同时自动运行时出现om.mdiaf.baf.BafException: Unknown class name: com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand

时间改为不同之后，自动运行不再报那个错误，但是也没进去（发现还是发生了相同的错误）
com.mdiaf.baf.BafException: Unknown class name: com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand

第一种
com.mdiaf.batch.exception.NoAlertException: 任务已经成功执行
第二种
[FCLOG] 15:48:00.014 [quartzScheduler_Worker-5] INFO  com.mdiaf.job T:4b1febb147e912e9 U: - [JBS] 421873224	nf南方接口健康性检查 开始执行！
[FCLOG] 15:48:04.282 [pool-1-thread-7] INFO  com.mdiaf.job T: U: - SPI-ALERT JobErrorNoRunListener listener begin
[FCLOG] 15:48:04.282 [pool-1-thread-7] INFO  com.mdiaf.job T: U: - SPI-ALERT go to jobErrorAlert
[FCLOG] 15:48:04.386 [pool-1-thread-7] INFO  com.mdiaf.job T: U: - SPI-ALERT alert add begin 
[FCLOG] 15:48:04.464 [pool-1-thread-7] INFO  com.mdiaf.job T: U: - SPI-ALERT alert add end {"startTime":"Aug 3, 2017 3:48:00 PM","errorMeg":"Unknown class name: com.mdiaf.recon.job.fund.nf.FundAdapterCheckCommand","host":"169.254.93.126","jobInstanceOid":425270732,"jobName":"nf南方接口健康性检查"}
[FCLOG] 15:48:04.464 [pool-1-thread-7] INFO  com.mdiaf.job T: U: - SPI-ALERT JobErrorNoRunListener listener end


http://172.16.1.131:8080
PasConfigParam Detail

name				Value			Description
JobExecutionMode	Cluster			Cluster:集群 Single：单点

TRIGGER_HOST		192.168.1.94	UAT:172.16.1.131










## java eclipse 注释代码快捷键 取消代码注释快捷键
注释掉代码：
把要注释的代码选中，
按Ctrl+Shift+/    /*  */  形式的
ctrl+/    //形式的
取消代码注释：
把要注释的代码选中，
按Ctrl+Shift+\   /*  */  形式的
ctrl+/   //形式的



#20170809

## class<T>和 class<?>类型 有什么区别
平时看java源代码的时候，如果碰到泛型的话，我想? T K V E这些是经常出现的，但是有时想不起来代表什么意思，今天整理下： 
？ 表示不确定的java类型。 
T  表示java类型。 
K V 分别代表java键值中的Key Value。 
E 代表Element。

Object跟这些东西代表的java类型有啥区别呢？ 
Object是所有类的根类，是具体的一个类，使用的时候可能是需要类型强制转换的，但是用T ？等这些的话，在实际用之前类型就已经确定了，不需要强制转换。

<？ extends Collection> 这里？代表一个未知的类型，
但是，这个未知的类型实际上是Collection的一个子类，Collection是这个通配符的上限.
举个例子
class Test <T extends Collection> { }

<T extends Collection>其中,限定了构造此类实例的时候T是一个确定类型(具体类型)，这个类型实现了Collection接口，
但是实现 Collection接口的类很多很多，如果针对每一种都要写出具体的子类类型，那也太麻烦了，干脆还不如用
Object通用一下。
<? extends Collection>其中,?是一个未知类型,是一个通配符泛型,这个类型是实现Collection接口即可。

经常在泛化的Class对象定义时看到
Class<T> xxx;
和
Class<?> xxx;
这样的代码，请问两者之间有什么区别？
Class<T>在实例化的时候，T要替换成具体类
Class<?>它是个通配泛型，?可以代表任何类型
<? extends T>受限统配，表示T的一个未知子类。
<? super T>下限统配，表示T的一个未知父类。

再比如说，用Class<?>[]时，数组里面的元素可以是任一的。
Class<?>[] clazzs = {PreferenceActivityTest.class, ExpandableListActivityTest.class};

##java.lang.Class
Class是一个Java类，跟java API中定义的诸如Thread、Integer类、我们自己定义的类是一样，也继承了Object（Class是Object的直接子类）。总之，必须明确一点，它其实只是个类，只不过名字比较特殊。更进一步说，Class是一个java中的泛型类型。

对于我们自己定义的类，我们用类来抽象现实中的某些事物，比如我们定义一个名称为Car的类来抽象现实生活中的车，然后可以实例化这个类，用这些实例来表示我的车、你的车、黄的车、红的车等等。

现在回到Class 类上来，这个类它抽象什么了？它的实例又表示什么呢？
在一个运行的程序中，会有许多类和接口存在。我们就用Class这个来来表示对这些类和接口的抽象，而Class类的每个实例则代表运行中的一个类。
例如，运行的程序有A、B、C三个类，那么Class类就是对A、B、C三个类的抽象。所谓抽象，就是提取这些类的一些共同特征，比如说这些类都有类名，都有对应的hashcode，可以判断类型属于class、interface、enum还是annotation。这些可以封装成Class类的域，另外可以定义一些方法，比如获取某个方法、获取类型名等等。这样就封装了一个表示类型(type)的类。



## Spring
下面列出的是使用 Spring 框架主要的好处：
- Spring 可以使开发人员使用 POJOs 开发企业级的应用程序。只使用 POJOs 的好处是你不需要一个 EJB 容器产品，比如一个应用程序服务器，但是你可以选择使用一个健壮的 servlet 容器，比如 Tomcat 或者一些商业产品。
- Spring 在一个单元模式中是有组织的。即使包和类的数量非常大，你必须并且只需要但是你需要的，而忽略剩余的那部分。
- Spring 不会让你白费力气做重复工作，它真正的利用了一些现有的技术，像几个 ORM 框架、日志框架、JEE、Quartz 和 JDK 计时器，其他视图技术。
- 测试一个用 Spring 编写的应用程序很容易，因为 environment-dependent 代码被放进了这个框架中。此外，通过使用 JavaBean-style POJOs，它在使用依赖注入注入测试数据时变得更容易。
- Spring 的 web 框架是一个设计良好的 web MVC 框架，它为 web 框架，比如 Structs 或者其他工程上的或者很少受欢迎的 web 框架，提供了一个很好的供替代的选择。
- 为将特定技术的异常（例如，由 JDBC、Hibernate，或者 JDO 抛出的异常）翻译成一致的， Spring 提供了一个方便的 API，而这些都是未经检验的异常。
- 轻量级的 IOC 容器往往是轻量级的，例如，特别是当与 EJB 容器相比的时候。这有利于在内存和 CPU 资源有限的计算机上开发和部署应用程序。
- Spring 提供了一个一致的事务管理界面，该界面可以缩小成一个本地事务（例如，使用一个单一的数据库）和扩展成一个全局事务（例如，使用 JTA）。
>POJO（Plain Ordinary Java Object）简单的Java对象，**实际就是普通JavaBeans**，是为了避免和EJB混淆所创造的简称。
>POJO是Plain OrdinaryJava Object的缩写不错，但是它通指没有使用Entity Beans的普通java对象，可以把POJO作为支持业务逻辑的协助类。
>POJO实质上可以理解为简单的实体类，顾名思义POJO类的作用是方便程序员使用数据库中的数据表，对于广大的程序员，可以很方便的将POJO类当做对象来进行使用，当然也是可以方便的调用其get,set方法。
>POJO有一些private的参数作为对象的属性。然后针对每个参数定义了get和set方法作为访问的接口。例如：
>```
>public class User {
>  private long id;
>  private String name;
>  public void setId(long id) {
>  	this. id = id;
>  }
>  public void setName(String name) {
>  	this. name=name;
>  }
>  public long getId() {
> 	 return id;
>  }
>  public String getName() {
>  	return name;
>  }
>}
>```







# 201708016



sourceTree 上切换分支	：保存直接切换，有冲突 解决冲突 不需要先提交再切换。

NFF-SFTP

[
drw-rw-rw   1     root     root         0 Aug 2 16:41 ., 
drw-rw-rw   1     root     root         0 Aug 2 16:41 .., 
-rw-rw-rw   1     root     root       125 Aug 1 15:14 800008_Application_20170801.txt, 
-rw-rw-rw   1     root     root     25099 Aug 1 15:16 800008_BatchTrans_20170801.txt, 
-rw-rw-rw   1     root     root        86 Aug 1 15:12 800008_CustomerRisk_20170801.txt, 
-rw-rw-rw   1     root     root       386 Aug 1 15:10 800008_payApplication_20170801.txt, 
-rw-rw-rw   1     root     root        81 Aug 1 15:18 800008_payConfirm_20170801.txt,
-rw-rw-rw   1     root     root       359 Aug 1 15:27 800008_ShopNotice_20170801.txt, 
-rw-rw-rw   1     root     root       114 Aug 1 16:30 800008_Transext_App_20170801.txt, 
drw-rw-rw   1     root     root         0 Aug 2 16:41 decrypt
]

获取文件名
.getfilename()

java数组
Java语言中提供的数组是用来存储固定大小的同类型元素。
你可以声明一个数组变量，如numbers[100]来代替直接声明100个独立变量number0，number1，....，number99。
本教程将为大家介绍Java数组的声明、创建和初始化，并给出其对应的代码。
**声明数组变量**
dataType[] arrayRefVar;
**创建数组**
arrayRefVar = new dataType[arraySize];
上面的语法语句做了两件事：
   一、使用dataType[arraySize]创建了一个数组。
   二、把新创建的数组的**引用**赋值给变量 arrayRefVar。
数组变量的**声明，和创建数组**可以用一条语句完成，如下所示：
dataType[] arrayRefVar = new dataType[arraySize];
或	dataType[] arrayRefVar = {value0, value1, ..., valuek};
数组的元素是通过索引访问的。数组索引从0开始，所以索引值从0到arrayRefVar.length-1。
**实例**
下面的语句首先声明了一个数组变量myList，接着创建了一个包含10个double类型元素的数组，并且把它的引用赋值给myList变量。
double[] myList = new double[10];
int[] array=new int[]{3, 1, 2, 6, 4, 2}
java.util.Arrays类能方便地操作数组，它提供的所有方法都是静态的。具有以下功能：
给数组赋值：通过fill方法。
对数组排序：通过sort方法,按升序。
比较数组：通过equals方法比较数组中元素值是否相等。
查找数组元素：通过binarySearch方法能对排序好的数组进行二分查找法操作。
用Iterator模式实现遍历集合
Iterator模式是用于遍历集合类的标准访问方法。它可以把访问逻辑从不同类型的集合类中抽象出来，从而避免向客户端暴露集合的内部结构。
Iterator模式总是用同一种逻辑来遍历集合：
      for(Iterator it = c.iterater(); it.hasNext(); ) { ... }
不论Collection的实际类型如何，它都支持一个iterator()的方法，该方法返回一个迭代子，使用该迭代子即可逐一访问Collection中每一个元素。典型的用法如下：
　　　　Iterator it = collection.iterator(); // 获得一个迭代子
　　　　while(it.hasNext()) {
　　　　　　Object obj = it.next(); // 得到下一个元素
　　　　}
　　由Collection接口派生的两个接口是List和Set。
　　
Collection
├List
│├LinkedList
│├ArrayList
│└Vector
│　└Stack
└Set
Map
├Hashtable
├HashMap
└WeakHashMap



# 20170818


## 功能快捷键
Home键与End键：快速定位到行首与行尾。 与shift键结合可以快速选定一整行。
Alt+上下 选中上下行
Ctrl+D：删除光标所在行货选取行。

## Tomcat web服务器

一个Java程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。
主方法入口：所有的Java 程序由public static void main(String args[])方法开始执行。


很多初学或将学**Java web**的朋友总是被一系列异于**常规java project**的流程结构所困惑，搞不清事情的本质，
这里就以最简单的方式来让初出茅庐的新手对Java web项目有个清晰明了的认识。

java项目运行于一个public类中的一个pulblic static void main（String[]）函数，然而java web中既没有了常规的main方法入口点同时各种纷乱的东西如jsp、html、tomcat以及servlet等也很容易让人陷入迷茫，就此使许多人在心中把java项目与web项目之间划起了天堑鸿沟。

简单写上一个简单的“tomcat”来帮助初学者把java web与常规java项目统一起来，以利于朋友们在最初就能对java web项目有个较常规的认识。

首先，我们来研究下java web项目的运行过程。
与普通java程序的main入口点不同，web似乎完全找不到了其入口点，然而需明确一点的是web项目中的servlet本身就是java类，同样是需要编译成.class被加载的，即使是jsp文件也是会经由jsp引擎转化为一个servlet被执行(html文件则仅被用来呆板的传输给双方浏览器解释)。所以web项目本质上还是一个java项目。

它与传统java项目的差异又该作何解释？
java项目根据程序流程触发，
web项目则是基于网络访问事件触发，故本质上是一个事件驱动系统，然而任何事件驱动系统本身还是有一个确定的入口的，这点web也不例外。入口是有的，main也是有的，只是这些东西都被隐藏了起来，就是tomcat(亦或是其他web容器)的入口。
这一点正如微软的MFC库封装了c++常规的main或WinMain入口一样，Tomcat也封装了java的main入口。

**动手写一个简单的tomcat仿真程序**
1.首先我们来创建一个java项目Tomcat，创建一个Servlet.MyServletIn接口，添加一个service方法，以模拟servlet中的service方法。
2.将我们的Servlet.MyServletIn接口导出为ServletPkg.jar文件作为我们的servlet库。
3.在项目根目录下添加TomcatConf.txt文件作为Tomcat的配置文件，这里简单起见采用普通文本而非Xml文件，此文件中存放两行内容 ，第一行所要部署servlet项目目录，第二行你自己的真实Servlet类名(包含包路径)。
4.创建一个Core.TomcatCore类，并在其中添加main，作为整个容器的入口，在main中完成初始化tomcat本身、通过TomcatConf.txt配置文件下的servlet文件系统路径及类包路径信息，加载所部署servlet等工作。
5.另创建一个java项目MyWeb(此项目不需要main，用来模拟我们的web项目，当然这里只有servlet而已。)
6.将我们的”Servlet库“ServletPkg.jar导入我们的”Web项目“。
7.在MyWeb中添加一个实现了MyServletIn接口的类MyServlet。
8.实现MyServlet的抽象方法service模仿真实Servlet的行为。
9.部署我们的"web项目“到我们的Tomcat，即将我们的"web项目"根下的bin路径写入Tomcat根下的配置文件(TomcatConf.txt)的第一行，并将我们的Servlet类名写入配置文件第二行。如下:
F:\Users\smy\workspace-eclipse\MyServlet\bin
MyWeb.MyServlet
10.运行我们的"tomcat"。





# 20170821



## 天安、国华、利安：南方基金划拨，



1，预生产地址：http://106.2.33.91/aiaf/login


生产环境只读账号
账号：zhonglangjin

密码：fcjr-001
2，设置--系统API管理--交易目标端口：NFF-SFTP，URL:121.35.255.69，USER ID：nf_product，Password：nf_product123456

3，winSCP：连接上，之后下载当天的 带有.bak的文件
4，对文件解码：用package com.mdiaf.recon.repository.test;  DecriptTransBatchMsgTest.java进行解码。
int size = decriptTransBatchMsgTest.countAmount("E:\\nanfang1\\", "800008_BatchTrans_20170821.txt.bak", "gbk", 2);
5，用解码后的文件代替bak文件



## SecureCRT乱码问题

选项--会话选项--外观--字符编码：UTF-8





## win7系统 “便笺” 如何设置字体大小

便签 在附件中。

增大字号/放大文本 Increased text size Ctrl+Shift+>
减小字号/缩小文本 Decreased text size Ctrl+Shift+<

粗体 Bold text Ctrl+B
斜体 Italic text Ctrl+I

下划线 Underlined text Ctrl+U
删除线 Strikethrough Ctrl+T

项目符号 Bulleted list Ctrl+Shift+L
(Press this keyboard shortcut again to switch to a numbered list.)再次使用此快捷键切换为数字项目符号

增大字号/放大文本 Increased text size Ctrl+Shift+>
减小字号/缩小文本 Decreased text size Ctrl+Shift+<





javaDoc

${}的是表达式，IDE会自动添加
这里`${date}`会自动添加上日期
```
 ${filecomment}
 ${package_declaration}
 /** 
 * @author  作者 E-mail:
 * @date 创建时间：${date} ${time}
 * @version 1.0
 * @parameter  
 * @since  
 * @return  
 */
 ${typecomment}
 ${type_declaration}
 
 
 ${filecomment}
 ${package_declaration}
  /** 
   *@date 创建时间：${date} ${time}
   *@author ${user}
   */
 ${typecomment}
 ${type_declaration}
 
 
 /**
 *@date 创建时间：2017年8月24日 下午2:02:35
 *@author shidexiao
 */
 
 
 
 
 eclipse中设置自动生成注释
 ${filecomment}
 ${package_declaration}
 中间加模板
 
 ${typecomment}
 ${type_declaration}
 
 
 
 
 * @date 创建时间：${date}  ${time} 
 * @version 1.0

/**
 * @date 创建时间：2017年8月24日 下午13：51：41
 * @version 1.0
 */
 
```






# 20170825

## eclipse中移除无用import有没有快捷键的
ctrl+shit+O:自动导入包，当然也会清除掉多余的包
eclipse中移除無用import有沒有快捷鍵的?
shift+ctrl+o，移除一样





# 20170828



## 与第三方（南方基金、上海农商行）的对接接口对比

南方基金的 “互联网基金销售平台对接协议”（我们使用的接口）是由金证财富南京科技有限公司写的

金证财富南京科技有限公司是金证股份的控股子公司，

深圳市金证科技股份有限公司成立于1998年，总部位于深圳。2003年12月24日，公司股票在上海证券交易所挂牌上市（股票代码：600446）。

金证股份是国家信息产业部认定的国家重点软件企业、国家系统集成一级资质单位，深圳市政府认定的高新技术企业，被科技部列入国家火炬计划软件园骨干企业。2013年金证在“互联网金融”领域的“余额宝”项目载入了金融IT发展史上的里程碑。并继“余额宝”之后，还联合腾讯推出“理财通”，将 “互联网金融”业务版块推向又一个新的高度。
金证在北京、上海、成都、南京和深圳设立了五个研发中心，市场营销和服务网络分为北方、华东（含华中）、西南、华南四大区域，覆盖全国20多个省市。

金证财富南京科技有限公司，金证财富成立于2013年9月。注册资本3000万元。主要从事包括基金公司、信托公司、证券资产管理、保险资产管理、期货资产管理、第三方专业理财及第三方支付在内的大资产管理行业客户的业务软件开发与系统集成服务。金证财富目前已经拥有近300余家总部级客户。其中包括30家新设公募基金公司总包，40家成熟公募基金公司；20家信托公司，40家证券公司，12家保险公司，6家期货公司，150余家第三方理财机构和5家支付机构客户。金证财富目前拥有员工530人，2016年底预计达到700人。技术团队中各产品领军人物大部分来自于金证股份原证券领域的核心团队。金证财富注册地在南京，办公地在深圳，在北京和上海设有分支机构，在南京和成都设有研发中心。



| 上海农商行（上海农商银行网络业务条线团队 ）                   | 南方基金（金证财富南京科技有限公司写，南方基金审批）               |
| ---------------------------------------- | ---------------------------------------- |
| SRCB_MSP_外联接入规范说明                        | 互联网基金销售平台对接协议（互联网直销接口）                   |
| 本规范 规定了互联网商户所使用的 上海农商银行MSP 发布的 金融服务 API，包括交易 类型 交易正常处理流程和异常情况的消息格 式以及交易报文格式说明 。 | 本文档描述了基金销售平台与电商对接的的技术接口方案。该方案主要定义了基金公司销售系统与第三方电商系统（如：网易金融、小米金融、腾讯金融等）平台之间业务交互中的数据格式。 |
| 报文传输：平台联机交易接口通过互联网HTTPS POST方式进行通讯，公共参数通过  URL params 方式传输，业务交易参数以**JSON**报文数据格式传输。 | 请求-应答模式  单向通知模式                          |
| HTTPS请求与响应消息中必须按照如下要求设置头部域："Content-Type"设置值：application/json;charset=utf-8;          URL params 中的每个value字段需要做urlenconde，防止签名验签出错。 | 系统交互报文规范：规定了基金支付平台与基金公司之间交换报文的顺序、格式与语义与处理规范。 |
| 签名验签：商户与上海农商行MSP交互时，为了保证数据传输过程中的数据的真实性和完整性，我们需要对数据进行加签（用自身持有的私钥对交易明文进行数字签名），在接收签名数据之后进行验签（用发送方的公钥对交易明文和密文进行校验）。 | 系统的请求采用HTTP同步请求，系统的请求、响应都使用**XML**格式。所有的系统报文均以Message作为根元素。Message元素中包含代表具体的元素。 |
| 签名：签名对象为请求实体JSON 字符串， 通过(ea_id).pfx 证书私钥使用**SHA256WithRSA 算法**加签。签名后的数据通过BASE64 编码转成字符串。将字符串通过URL params 的signature 字段传递到服务端。 | 报文加密：为保证系统间通讯的安全性，接口请求和响应均需要对参数进行加密处理，报文使用基金公司与支付公司约定的密钥进行加密之后再发送，采用MD5算法进行签名。 |
| 验签：验签对象为读取Response原始数据流方式获得的JSON格式的数据字符串。通过srcbmsp.cer证书获取公钥，使用SHA256WithRASA算法对字符串进行签名与Response返回headers信息中signature的值进行对比验签。 | 报文传输：系统交互报文的传输使用XML Over HTTP方式，在HTTP请求/响应体中包含XML形式的报文。对HTTP传输的基本要求如下：消息请求基于HTTP的POST方式。HTTP请求与响应消息中必须按照如下要求设置头部域： |
| 联机请求交易说明：交易列表                            |                                          |
| 联机推送交易说明：联机推送交易 主要为 MSP 主动推送接入商户的联机交易，   |                                          |
| 外联业务异步通知接口：二类账户开、充值交易结果异步通知 。                                                               文件推送接口：批量代付回盘、充值提现对 账、支付退款对账文本推送。 |                                          |
| 附录：公共响应码                                           文本数据格式 |                                          |
|                                          |                                          |







我们nfs系统 按照开发环境搭建过程 没有安装maven过程

先安装一下maven：解压--maven_home, path

在此处打开命令窗口（cmd）：shift+右键

## 解决冲突

今天 解决冲突

先是在文本编辑器里面 修改了冲突 后 不知怎么出了问题

后来 提交那个合并  竟然好了





# 20170830



web、逻辑层：

service层：

dto层：数据传输对象（DTO)(Data Transfer Object)

dao层：DAO(Data Access Object) 数据访问对象





# 20170831



### MVC与三层架构

通过昨天songyuhua跟我说了dto、与事务管理的含义，一下子把我对整个系统架构的理解，再联系之前的ORM改造，一切都串起来了。



表现层：UI（User Interface）层

业务逻辑层：BL（Business Logic）层

数据访问层：DA（Data Access）层



### Java工程中几种常见的包：PO，VO，DAO，BIZ,DTO,Service,ServiceImpl

一、PO:persistant object 持久对象,是与[数据库](http://lib.csdn.net/base/mysql)中的表相映射的[Java](http://lib.csdn.net/base/java)对象。最简单的PO就是对应数据库中某个表中的一条记录，多个记录可以用PO的集合。PO中应该不包含任何对数据库的操作。 
二、VO:value object值对象。通常用于业务层之间的数据传递，和PO一样也是仅仅包含数据而已。但应是抽象出的业务对象,可以和表对应,也可以不,这根据业务的需要。 
三、POJO:plain ordinary [Java ](http://lib.csdn.net/base/java)object ,简单无规则java对象，只有一些属性和属性对应的setter和getter方法，tostring（）方法，前面提到的PO和VO都可以归为POJO. 
四、DTO:data transfer object 数据传输对象，有时我们仅仅需要获得某个表的几个字段，所以此时用PO对象就有点大材小用了，我们就可以用DTO来存储这几个字段。可以把它理解为VO 
五、DAO:data access object 数据访问对象，此对象用于访问数据库。通常和PO结合使用，DAO中包含了各种数据库的操作方法。通过它中的方法,结合PO对数据库进行相关的操作。 
六.BIZ:其名称就是商业的简写，也就是其对应的是业务层，此包里的对象通过调用DAO中的对象里的方法来完成业务层上的操作，其目的是封装对数据库的操作。 
七、Service: 我现在做的项目里是在这个包里只放接口，有的是把此包当成业务层biz， 
八、ServiceImpl : 此包中的对象为实现Service里的接口类

以上提到的这几个概念是以工程中包的角度来解释的，也就是说工程中的包名字的最后一个字段是以dao，pojo，biz等等来命名的

下面简单介绍一下java中各个层次：

Modle 模型层 ：存放你的实体类 
Dao ：主要做数据库的交互工作 
Biz ：做相应的业务逻辑处理 
Action：是一个控制器

Modle 模型层 ：一般是实体对象(把现实的的事物变成java中的对象，对应前面提到的po，vo，dto)，作用是暂时存储数据方便持久化（存入数据库或者写入文件）

Dao 数据访问层 ： 就是用来访问数据库实现数据的持久化（把内存中的数据永久保存到硬盘中 ）

Biz 也叫做Service层：在此层做相应的业务逻辑处理

Action层：业务层的一部分，是一个管理器 （总开关）（作用是取掉转）（取出前台界面的数据，调用biz方法，转发到下一个action或者页面）



### 我们公司的架构

每个项目 都有com.msiaf....的包

通过这些包组织程序

目前看没有看到 不同项目之间的联系，但是结合前些天 我看的那个自己动手写tomcat，当时也是两个项目，但是他们通过在Tomcat中的配置文件中添加配置文件

E:\workspace-test\MyWeb\bin
MyWeb.MyServlet

在MyWeb项目的src.MyWeb包的MyServlet.java文件中实现MyServletIn这个接口，这个借口是来自ServletPkg.jar这个jar包里的serlet包下的一个接口，这个jar包来自Tomcat的src.Servlet,里面一个MyServletIn.java的接口程序。

至此我发现 不同项目的联系可以通过打jar包和配置文件实现。



公司架构下面，操作数据库的方法的类本应放在DAO中，但是我们这边没有dao包，然后放在了service中，然后调用这些DAO类的对象放在service中。

这里就是

public interface BmfAggrManager extends BmfObjectManager, BmfAggrRepository {

@Service
@Transactional
public class BmfAggrManagerImpl extends BmfObjectManagerImpl implements BmfAggrManager {

public interface BmfOrmAggrManager {

@Service
public class BmfOrmAggrManagerImpl implements BmfOrmAggrManager {

这些类放在了aiaf-bcf中的com.mdiaf.bmf.service中

而调用这些对象的类放在各个项目的service中

像aiaf-ayb下的com.mdiaf.fsa.service中就有调用上面的dao对象。

 

PO、VO、POJO与DTO是在DTO的包里面，供DAO使用。



bean可以跨项目访问 通过@autowired     注入可以快速用到 某个对象实例





## 张孝祥

因为有几本很好的书，买来之后 阅读发现写的很好 发现作者是张孝祥，所以就多搜了一下 了解

系统环境变量就是在操作系统中定义的变量，可供操作系统上的所有应用程序使用。

shidexiao的用户变量、系统变量：区别是上面的窗口的设置用于个人环境变量，只有以该用户身份登陆系统时才有效，而下面窗口中的设置则对所有用户都有效。





# 20170901



都注意下，代码里面所有时间处理的都用BafDateUtils里面的，绝对禁止私自单独写方法

有需要的在BafDateUtils里面新增方法





# 20170904

## @Resource @Autowired @component byType byName

@Resource
```
@Component
public class NffundTradeListener implements IMessageListener {
	@Autowired
	private BmfOrmAggrManager bmfOrmAggrManager;
```


```
@Component
public class FundInterfaceListener extends AbstractRabbitMultiMessageListener {
	private Logger logger = LoggerFactory.getLogger(NFSLogType.SPI);
	@Resource
	private IMessageListener nffundTradeListener;
```

@Autowired
```
public interface NewSrcBankService {
```

```
@Service
public class NewSrcBankServiceImpl implements NewSrcBankService {
	@Autowired
    private BmfOrmAggrManager bmfOrmAggrManager;
```

```
@Component("newSrcbTransVerifyRequestConvert")
public class NewSrcbTransVerifyRequestConvert implements FundBeanConvert<SingleQueryRequest, NewSrcbTransVerifyRequest> {
	@Autowired
	private NewSrcBankService newSrcBankService;
```

@autowired
private 接口 实例名

##spring mvc
