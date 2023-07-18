## "Distributed Task Scheduling Platform XXL-JOB"

[![Actions Status](https://github.com/xuxueli/xxl-job/workflows/Java%20CI/badge.svg)](https://github.com/xuxueli/xxl-job/actions)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.xuxueli/xxl-job/badge.svg)](https://maven-badges.herokuapp.com/maven -central/com.xuxueli/xxl-job/)
[![GitHub release](https://img.shields.io/github/release/xuxueli/xxl-job.svg)](https://github.com/xuxueli/xxl-job/releases)
[![GitHub stars](https://img.shields.io/github/stars/xuxueli/xxl-job)](https://github.com/xuxueli/xxl-job/)
[![Docker Status](https://img.shields.io/docker/pulls/xuxueli/xxl-job-admin)](https://hub.docker.com/r/xuxueli/xxl-job-admin /)
[![License](https://img.shields.io/badge/license-GPLv3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0.html)
[![donate](https://img.shields.io/badge/%24-donate-ff69b4.svg?style=flat)](https://www.xuxueli.com/page/donate.html)

[TOCM]

[TOC]

## 1. Introduction

### 1.1 Overview
XXL-JOB is a distributed task scheduling platform. Its core design goals are rapid development, easy learning, lightweight, and easy expansion. The source code is now open and connected to the online product lines of many companies, out of the box.

### 1.2 Community Communication
- [Community Exchange](https://www.xuxueli.com/page/community.html)

### 1.3 Features
- 1. Simple: Support CRUD operations on tasks through web pages, easy to operate, and get started in one minute;
- 2. Dynamic: Supports dynamic modification of task status, start/stop task, and termination of running tasks, which take effect immediately;
- 3. Dispatch Center HA (Central): The dispatch adopts a central design. The "Dispatch Center" self-develops dispatch components and supports cluster deployment, which can ensure the dispatch center HA;
- 4. Executor HA (distributed): task distributed execution, task "executor" supports cluster deployment, which can ensure task execution HA;
- 5. Registration center: The executor will automatically register tasks periodically, and the dispatch center will automatically discover the registered tasks and trigger execution. At the same time, it also supports manual entry of the executor address;
- 6. Flexible expansion and contraction: Once a new executor machine goes online or offline, tasks will be reassigned in the next scheduling;
- 7. Trigger strategy: Provide rich task trigger strategies, including: Cron trigger, fixed interval trigger, fixed delay trigger, API (event) trigger, manual trigger, parent-child task trigger;
- 8. Scheduling expiration strategy: the compensation processing strategy for the dispatch center to miss the dispatch time, including: ignore, immediately compensate and trigger once, etc.;
- 9. Blocking processing strategy: the processing strategy when the scheduling is too intensive and the executor is too late to process. The strategies include: single-machine serial (default), discarding subsequent scheduling, and overriding previous scheduling;
- 10. Task timeout control: Support custom task timeout time, task running timeout will actively interrupt the task;
- 11. Task failure retry: support custom task failure retry times, when the task fails, it will take the initiative to retry according to the preset failure retry times; among them, fragmentation tasks support fragmentation granularity failure retry;
- 12. Task failure alarm; email failure alarm is provided by default, and an expansion interface is reserved at the same time, which can easily expand SMS, DingTalk and other alarm methods;
- 13. Routing strategy: Rich routing strategies are provided when the executor cluster is deployed, including: first, last, polling, random, consistent HASH, least frequently used, least recently used, failover, busy transfer wait;
- 14. Fragmented broadcast task: When the executor cluster is deployed, if the task routing strategy selects "fragmented broadcast", a task schedule will broadcast and trigger all executors in the cluster to execute a task, and the fragmentation can be developed according to the fragmentation parameters Task;
- 15. Dynamic sharding: shard broadcast tasks are sharded in the dimension of executors, and support dynamic expansion of executor clusters to dynamically increase the number of shards and coordinate business processing; tasks can be significantly improved when performing large-scale business operations processing power and speed.
- 16. Failover: When the task routing policy selects "Failover", if a machine in the executor cluster fails, it will automatically failover and switch to a normal executor to send scheduling requests.
- 17. Task progress monitoring: support real-time monitoring of task progress;
- 18. Rolling real-time log: support online viewing of scheduling results, and support real-time viewing of the complete execution log output by the executor in Rolling mode;
- 19. GLUE: Provides Web IDE, supports online development of task logic code, dynamic release, real-time compilation and effect, omitting the process of deployment and online. Backtracking of 30 versions of historical versions is supported.
- 20. Script tasks: support the development and operation of script tasks in GLUE mode, including Shell, Python, NodeJS, PHP, PowerShell and other types of scripts;
- 21. Command line task: natively provide a general command line task Handler (Bean task, "CommandJobHandler"); the business side only needs to provide the command line;
- 22. Task dependency: Support configuration of subtask dependencies. When the execution of the parent task is completed and the execution is successful, it will actively trigger the execution of a subtask. Multiple subtasks are separated by commas;
- 23. Consistency: "Scheduling Center" ensures the consistency of cluster distributed scheduling through DB locks, and a task scheduling will only trigger one execution;
- 24. Custom task parameters: support online configuration scheduling task input parameters, which take effect immediately;
- 25. Scheduling thread pool: multi-threaded scheduling system triggers scheduling operation to ensure accurate execution of scheduling without being blocked;
- 26. Data encryption: The communication between the dispatching center and the actuator is encrypted to improve the security of dispatching information;
- 27. Email alarm: support email alarm when the task fails, and support the configuration of multiple email addresses to send alarm emails;
- 28. Push maven central warehouse: the latest stable version will be pushed to maven central warehouse, which is convenient for users to access and use;
- 29. Operation report: support real-time viewing of operation data, such as the number of tasks, scheduling times, number of executors, etc.; and scheduling reports, such as scheduling date distribution diagram, scheduling success distribution diagram, etc.;
- 30. Fully asynchronous: The task scheduling process is fully asynchronously designed and implemented, such as asynchronous scheduling, asynchronous operation, asynchronous callback, etc., which can effectively cut traffic peaks for intensive scheduling, and theoretically support the operation of tasks of any duration;
- 31. Cross-language: The dispatch center and the executor provide language-independent RESTful API services, and any third-party language can connect to the dispatch center or implement the executor. In addition, it also provides other cross-language solutions such as "multitasking mode" and "httpJobHandler";
- 32. Internationalization: The dispatch center supports internationalization settings, providing two optional languages, Chinese and English, and the default is Chinese;
- 33. Containerization: provide the official docker image, and update and push dockerhub in real time, further realizing the out-of-the-box use of the product;
- 34. Thread pool isolation: The scheduling thread pool is isolated and split, and slow tasks are automatically downgraded to the "Slow" thread pool to avoid exhausting scheduling threads and improve system stability;
- 35. User management: support online management system users, there are two roles of administrator and ordinary user;
- 36. Permission control: Permission control is performed in the executor dimension, administrators have full permissions, and ordinary users need to be assigned executor permissions before allowing related operations;

### 1.4 Development
In mid-2015, I created the XXL-JOB project warehouse on github and submitted the first commit, followed by system structure design, UI selection, interaction design...

From 2015 to November, XXL-JOB finally released the first major version V1.0, and then I released it to OSCHINA. XXL-JOB was recommended by @甜蜜 on OSCHINA, and reached OSCHINA’s " "Hot Action" ranks first and git.oschina's open source software ranks first in monthly popularity. Here, I would like to thank Sweet Potato and thank you for your attention and support.

From December 2015, I published XXL-JOB to our internal knowledge base, which was recognized by internal colleagues.

In January 2016, our company started the internal access and customization of XXL-JOB. I would like to thank Yuan and Yin for their contributions, and also thank other internal colleagues for their attention and support.

On 2017-05-13, in the "62nd Open Source China Source Innovation Conference" (https://www.oschina.net/event/2236961)" held in Shanghai, I took the stage to challenge XXL -JOB gave a speech, and the audience of 500 people responded enthusiastically ([Graphic Review](https://www.oschina.net/question/2686220_2242120) ).

On 2017-10-22, I also participated in the "[Advance Microservice Practical School Shanghai Station] (https://opentalk.upyun.com/303.html)" held by Open Talk and the Spring Cloud Chinese community. XXL-JOB made a speech, the audience responded enthusiastically and discussed and exchanged with XXL-JOB users after the meeting.

On 2017-12-11, XXL-JOB had the honor to participate in "[InfoQ ArchSummit Global Architects Summit] (http://bj2017.archsummit.com/)", and was patted by "Mr. Yang Bo", the architecture director of Paipai Loan, in the topic " [Microservice Principles, Infrastructure and Open Source Practice](http://bj2017.archsummit.com/training/2)" Introduced on site.

On 2017-12-18, XXL-JOB participated in the evaluation of "[2017 Most Popular Chinese Open Source Software](http://www.oschina.net/project/top_cn_2017?sort=1)", about Competed among 9,000 domestic open source projects, and finally entered the top 30.

On January 15, 2018, XXL-JOB participated in the evaluation of "[2017 Code Cloud Hottest Open Source Project](https://www.oschina.net/news/92438/2017-mayun-top-50)", which was already Competed in about 6,500 code cloud projects entered, and finally entered the top 20.

On 2018-04-14, iTechPlus held "[2018 Internet Developers Conference](http://www.itdks.com/eventlist/detail/2065)" in Shanghai, I gave a speech to XXL-JOB on the stage. The audience responded enthusiastically and discussed and exchanged with XXL-JOB users after the meeting.

On May 27, 2018, in the "Architecture" theme session of "[The 75th Open Source China Source Creation Conference](https://www.oschina.net/event/2278742)" held in Shanghai, I took the stage to conduct "Basic Architecture and Middleware Graph" keynote speech, thousands of audiences responded enthusiastically ([graphic review](https://www.oschina.net/question/3802184_2280606) ).

On 2018-12-05, XXL-JOB participated in the evaluation of "[2018 Most Popular Chinese Open Source Software](https://www.oschina.net/project/top_cn_2018?sort=1)", among the More than 10,000 open source projects competed and finally ranked 19th.

On 2019-12-10, XXL-JOB participated in the "[2019 Most Popular Chinese Open Source Software](https://www.oschina.net/project/top_cn_2019)" evaluation, and more than 10,000 open source software had been entered at that time Competing in the project, and finally ranked 9th in "Development Framework and Basic Components".

On November 16, 2020, XXL-JOB participated in the evaluation of "[The Most Popular Chinese Open Source Software in 2020](https://www.oschina.net/project/top_cn_2020)". Competing in the project, and finally ranked 8th in "Development Framework and Basic Components".

On 2021-12-06, XXL-JOB participated in the "[2021 OSC China Open Source Project Selection](https://www.oschina.net/project/top_cn_2021)" evaluation, and more than 10,000 open source projects had been entered at that time In the competition, it was finally selected as the "Most Popular Project".

> Our company Dianping has now connected to XXL-JOB, and its internal alias is "Ferrari" (Ferrari is customized based on the V1.1 version of XXL-JOB, and it is recommended to upgrade to the latest version for new access applications).
According to the latest statistics, from 2016-01-21 to 2017-12-01, the system has dispatched about 1 million times, which is an excellent performance. It is recommended to use the latest version for new access applications, because after dozens of version updates, the system's task model, UI interaction model, and underlying scheduling communication model have been greatly optimized and improved, and the core functions are more stable and efficient.

So far, XXL-JOB has been connected to the online product lines of many companies, and access scenarios such as e-commerce business, O2O business and big data operations, etc. As of the latest statistical time, the companies that XXL-JOB has connected include but are not limited to :

- 1. Dianping [Meituan Dianping]
- 2. Shandong Xueer Network Technology Co., Ltd.;
- 3. Anhui Huitong Internet Technology Co., Ltd.;
- 4. Renren Jucai Financial Service;
- 5. Shanghai Tangdi Information Technology Co., Ltd.
- 6. Yunmanman【Yunmanman】
- 7. Michelin (China)【Michelin】
- 8. Mother Alliance
- 9. Jiuying Tianxia (Beijing) Information Technology Co., Ltd.
- 10. OnePlus Technology Co., Ltd. 【OnePlus】
- 11. Shanghai Yibao Health Management Co., Ltd.
- 12. Haier Xinchu [Haier]
- 13. Henan Big Red Packet E-Commerce Co., Ltd.
- 14. Chengdu Shundian Technology Co., Ltd.
- 15. Shenzhen Eternal Asia
- 16. Shenzhen Maiyaxin Technology Co., Ltd.
- 17. Shanghai Boying Technology Information Technology Co., Ltd.
- 18. China Ping An Technology Co., Ltd. [Ping An of China]
- 19. Hangzhou Zhishi Information Technology Co., Ltd.
- 20. Boying Technology (Shanghai) Co., Ltd.
- 21. Chengdu Eneng Co., Ltd.
- 22. Hunan Gaoyang Tonglian Information Technology Co., Ltd.
- 23. Shenzhen Bond Culture Development Co., Ltd.
- 24. Fujian Asco Network Education Co., Ltd.
- 25. Uxin used car [Uxin]
- 26. Shanghai Youyoutang Investment Development Co., Ltd. [Youyoutang]
- 27. Beijing Chabi Lantian Technology Co., Ltd.
- 28. Zhongxiu Technology (Wuxi) Co., Ltd.
- 29. Wuhan Hollow Technology Co., Ltd.
- 30. Beijing Ant Storm Technology Co., Ltd.
- 31. Sichuan Huyida Technology Co., Ltd.
- 32. Wallet Cloud (Beijing) Technology Co., Ltd.
- 33. Chongqing Xincai Group
- 34. Migu Interactive Entertainment Co., Ltd. [China Mobile]
- 35. Beijing Noitom Technology Co., Ltd.
- 36. Growth Engine (Beijing) Information Technology Co., Ltd.
- 37. Beijing Inbes Technology Co., Ltd.
- 38. Gangtai Group
- 39. Shenzhen Taijiu Information System Co., Ltd.
- 40. Vivepay Payment Co., Ltd.
- 41. Guangzhou Hannong Network Technology Co., Ltd.
- 42. Xiangdian Technology Co., Ltd.
- 43. Hangzhou Bizhi Technology Co., Ltd.
- 44. Shenzhen Critical Line Network Technology Co., Ltd.
- 45. Guangzhou Knowledge Circle Network Technology Co., Ltd.
- 46. KOKUYO Commercial Shanghai Co., Ltd.
- 47. Haier Consumer Finance Co., Ltd., Hipay, Gouhua [Haier]
- 48. Guangzhou Batulu Information Technology Co., Ltd.
- 49. Shenzhen Penghaiyun Electronic Data Interchange Co., Ltd.
- 50. Shenzhen Yafei Electronic Commerce Co., Ltd.
- 51. Shanghai Quyi Network Co., Ltd.
- 52. Jujin Capital
- 53. Beijing Parent State Network Technology Co., Ltd.
- 54. Zhongshan Yuanhe Software Technology Co., Ltd.
- 55. Zhongshang Huimin (Beijing) E-Commerce Co., Ltd.
- 56. Kaijing Group
- 57. Huaxia Piaolian (Beijing) Technology Co., Ltd.
- 58. Paipaidai [Paipaidai]
- 59. Beijing Suntech Institution Online Education Co., Ltd.
- 60. Renzihang Co., Ltd.
- 61. Beijing Time E-Commerce Co., Ltd.
- 62. Shenzhen Juanpi Network Technology Co., Ltd.
- 63. Beijing Anbotong Technology Co., Ltd.
- 64. Future wireless network
- 65. Xiamen Cixi Network Co., Ltd.
- 66. Beijing Dilanke Software Co., Ltd.
- 67. Zhengzhou Chuanghai Software Technology Company
- 68. Beijing Guohuai Information Technology Co., Ltd.
- 69. Inspur Software Group
- 70. Doliheng (Beijing) Information Technology Co., Ltd.
- 71. Guangzhou Jixunke Information Technology Co., Ltd.
- 72. Trendy (China) Group Co., Ltd.
- 73. Haitouhui
- 74. Shanghai Runyi Entrepreneurship Incubator Management Co., Ltd.
- 75. Hannason (Xiamen) Data Co., Ltd.
- 76. Anxin Trust
- 77. Lan Ru Wealth
- 78. Jiedao Software
- 79. Hubei Xiangqi Network Technology Co., Ltd.
- 80. Hunan Chuangfa Technology Co., Ltd.
- 81. Shenzhen Xiaoan Times Internet Financial Services Co., Ltd.
- 82. Hubei Xiangqi Network Technology Co., Ltd.
- 83. Wallet Cloud (Beijing) Technology Co., Ltd.
- 84. 360 Finance [360]
- 85. Yiqixiu
- 86. Mobei (Shanghai) Biotechnology Co., Ltd.
- 87. Guangdong Core Wisdom Technology Co., Ltd.
- 88. Lenovo Group [Lenovo]
- 89. Monster charging
- 90. Xingyuan Automobile
- 91. Shenzhen Diandiantong Technology Mailbox Company
- 92. Jingdong [Jingdong]
- 93. Mizhuang Financial Management
- 94. Coffee is easy to melt
- 95. Wutong Chengxuan
- 96. Evergrande Real Estate [Evergrande]
- 97. Kunming Longhui
- 98. Shanghai Shiyao Software
- 99. Yixin【NetEase】
- 100. Tongban Street
- 101. Hangzhou Yunruo Network Technology Co., Ltd.
- 102. Tupperware (China) Co., Ltd.
- 103. Changshan Zhongka Yunli Supply Chain Management Co., Ltd.
- 104. Shenzhen Lichuang Electronic Commerce Co., Ltd.
- 105. Hangzhou Zhinuo Technology Co., Ltd.
- 106. Beijing Yunyang Information Technology Co., Ltd.
- 107. Shenzhen Duoyin Technology Co., Ltd.
- 108. dear baby
- 109. Shanghai Boka Software Technology Co., Ltd.
- 110. Wisdom Tree Online Education Platform
- 111. Mi Finance
- 112. Beijing Chensen Century
- 113. Yunnan Dianyitong
- 114. Guangzhou Fenling Network Technology Co., Ltd.
- 115. Zhejiang Micro Energy Technology Co., Ltd.
- 116. Shanghai Xinfei Electronic Commerce Co., Ltd.
- 117. Shanghai Baozun Electronic Commerce Co., Ltd.
- 118. Zhiketong Technology Co., Ltd.
- 119. Kedu Technology Co., Ltd.
- 120. Shanghai Shuhui System Technology Co., Ltd.
- 121. My Medicine Network
- 122. Multi-powder platform
- 123. Armored second-hand mobile phone
- 124. Shanghai Haixinde Data Technology Co., Ltd.
- 125. Shenzhen Zhenaiwang Information Technology Co., Ltd. [Zhenaiwang]
- 126. Little bee
- 127. Jirong Digital Technology
- 128. Shanghai Kaiyu Information Technology Co., Ltd.
- 129. Guangzhou Lizhi Network Co., Ltd. [Lichi FM]
- 130. Hangzhou Shanbao Technology Co., Ltd.
- 131. Beijing Internet New Network Technology Development Co., Ltd.
- 132. Yudao Technology
- 133. Shanxi Zhaosheng Real Estate Development Co., Ltd.
- 134. Beijing Lanrui Tongda Technology Co., Ltd.
- 135. Moon House (China) Co., Ltd. [Blue Moon]
- 136. Qingdao Guorui Information Technology Co., Ltd.
- 137. Boya Cloud Computing (Beijing) Co., Ltd.
- 138. Huatai Securities Hong Kong Subsidiary
- 139. Hangzhou East Communication Software Technology Co., Ltd.
- 140. Wuhan Bosheng Security Technology Co., Ltd.
- 141. Shenzhen Liudu Renhe Technology Co., Ltd.
- 142. Hangzhou Quwei Technology Co., Ltd. (Xiaoying)
- 143. Ningbo Cycling Man Home Technology Co., Ltd. [Cycling Man]
- 144. Dingding Yunkang Information Technology (Beijing) Co., Ltd.
- 145. Cloud money bag
- 146. Nanjing Zhongxing Liwei
- 147. Shanghai Sichang Communication Technology Co., Ltd.
- 148. Shenzhen Sacco Technology
- 149. China Comservice Founded Technology Co., Ltd.
- 150. Shenzhen Duzhuang Technology Co., Ltd.
- 151. Shanghai Stock Exchange Information Network Co., Ltd.
- 152. Hangzhou Huoshaoyun Technology Co., Ltd. [Wedding]
- 153. Tianjin Green Mango Technology Co., Ltd. [Mango Headlines]
- 154. YOFC Optical Fiber & Cable Co., Ltd.
- 155. Century Kaige (Beijing) Medical Technology Co., Ltd.
- 156. Zhejiang Linzi Holdings Co., Ltd.
- 157. Jiangxi Tengfei Network Technology Co., Ltd.
- 158. Anxun Logistics Co., Ltd.
- 159. The Internet of Meat
- 160. Beijing Beiguang Tiying Advertising Media Co., Ltd.
- 161. Shanghai Shuhui System Technology Co., Ltd.
- 162. Great Aspirations
- 163. Shanghai Yunque Medical
- 164. Shanghai Yunque Medical
- 165. Ink Weather [Ink Weather]
- 166. Shanghai Yicheng Information Technology Co., Ltd.
- 167. 
- 168. Hangzhou Hang Seng Yunrong Network Technology Co., Ltd.
- 169. Green Rice Lianchuang
- 170. Chongqing Yichong Technology Co., Ltd.
- 171. Anhui Pilot Technology Co., Ltd. (Lezhi.com)
- 172. Shanghai Shulian Medical Information Enterprise Development Co., Ltd.
- 173. Liangbin Building Materials
- 174. Hangzhou Qiushi Tongchuang Network Technology Co., Ltd.
- 175. Homer International
- 176. Yuanpeng IoT
- 177. Shenzhen Huaxing Optoelectronics Technology Co., Ltd.
- 178. Xiamen Shenzhou Eagle Software Technology Co., Ltd.
- 179. Shenzhen China Merchants Cigna Life Insurance Co., Ltd.
- 180. Shanghai Haowuwang Information Technology Co., Ltd.
- 181. Hisense Group [Hisense]
- 182. Xinlingke Information Technology (Shanghai) Co., Ltd.
- 183. Changchuncheng Technology Development Co., Ltd.
- 184. UFIDA Financial Information Technology Co., Ltd. [UFIDA]
- 185. Beijing Coffee Yirong Co., Ltd.
- 186. SDIC UBS Fund Management Co., Ltd.
- 187. Jinsong (Shanghai) Network Information Technology Co., Ltd.
- 188. Shenzhen Suishou Technology Co., Ltd. [Suishouji]
- 189. Shenzhen Water Technology Co., Ltd.
- 190. Yiqixiu [Yiqixiu]
- 191. Beijing Ciyun Technology
- 192. Nanjing Fengtai Internet Technology Co., Ltd.
- 193. Octopus Live
- 194. Award Duoduo Technology
- 195. Tianjin Shenzhou Shanglong Technology Co., Ltd.
- 196. Core Technology
- 197. Chema Technology (Beijing) Co., Ltd.
- 198. Guiyang Investment Holding Group
- 199. Kangqi shares
- 200. Longteng travel
- 201. Hangzhou Hualiang Software
- 202. Hefei Dingling Medical Technology Co., Ltd.
- 203. Chongqing Expression Technology Co., Ltd.
- 204. Shanghai Midao Information Technology Co., Ltd.
- 205. Beijing Yiyouhui Technology Co., Ltd.
- 206. Beijing Rongguan E-Commerce Co., Ltd.
- 207. China Foreign Exchange Trading Center
- 208. Sinotrans Co., Ltd.
- 209. China Shanghai Xiaoquan Education Technology Co., Ltd.
- 210. Pulian Software Co., Ltd.
- 211. Beijing Kelan Software Co., Ltd.
- 212. Jiangsu Snow IoT Technology Co., Ltd.
- 213. Beijing Sohu-Fox Friends [Sohu]
- 214. Newland Online Merchant Finance
- 215. Shandong Shenma Zhongshui Information Technology Co., Ltd.
- 216. Henan Huishun Network Technology Co., Ltd.
- 217. Beijing Huaxia Siyuan Technology Development Co., Ltd.
- 218. Shanghai Dongpu Information Technology Co., Ltd.
- 219. Shanghai Mingbo Network Technology Co., Ltd.
- 220. Guangdong Xueyuan Education Development Co., Ltd.
- 221. Shenzhen Qiangshi Technology Co., Ltd.
- 222. Shanghai Yunli Information Technology Co., Ltd.
- 223. Chongqing Yukehang Network Co., Ltd.
- 224. Number of clouds
- 225. State Grid Transportation Inspection Department
- 226. Hangzhou Find Fun
- 227. Haojing Cloud Computing Technology Co., Ltd.
- 228. Keda Xunfei [Kustek Xunfei]
- 229. Hangzhou Xingzhuang Network Technology Co., Ltd.
- 230. Instant installment financing
- 231. Shenzhen Fasid Information Technology Co., Ltd.
- 232. Shanghai Bofu Information Technology Co., Ltd.
- 233. Hangzhou Yunjia Cloud Computing Co., Ltd.
- 234. Youjia Homestay (Youjia Meisu)
- 235. Beijing Yingshaotong Software Technology Co., Ltd.
- 236. Zhejiang Juyoucai Financial Service Outsourcing Co., Ltd.
- 237. Yizu Zhihui (Beijing) Technology Co., Ltd.
- 238. Hefei Dingling Medical Technology Development Co., Ltd.
- 239. Chechuanbao (Shenzhen) Xuheng Technology Co., Ltd.)
- 240. Guangzhou R & F Real Estate Co., Ltd.
- 241. Hydrogen Class (Shanghai) Education Technology Co., Ltd.
- 242. Wuhan Krypton Cell Network Technology Co., Ltd.
- 243. Hangzhou Youyun Technology Co., Ltd.
- 244. Shanghai Xiandou Intelligent Robot Co., Ltd.
- 245. Lakala Payment Co., Ltd. [Lakala]
- 246. Hucai Printing Arts Co., Ltd.
- 247. Beijing Shuwei Technology Co., Ltd.
- 248. Guangdong Zhirui Technology Co., Ltd.
- 249. Find steel mesh
- 250. Nine Machine Network
- 251. Hangzhou Paopao Network Technology Co., Ltd.
- 252. Shenzhen Future Gathering
- 253. Hangzhou Daily Geili Technology Co., Ltd.
- 254. Shanghai Qiben Information Technology Co., Ltd.
- 255. Didi Chuxing [Didi]
- 256. Hefei Yundiagnosis Information Technology Co., Ltd.
- 257. Yunzhisheng Intelligent Technology Co., Ltd.
- 258. Nanjing Tandao Technology Co., Ltd.
- 259. Aileyou (second-hand platform)
- 260. Maoyan Movie (privatized deployment) [Maoyan Movie]
- 261. Meituan Elephant (Privatization Deployment) [Meituan Elephant]
- 262. Zuoyuebang Educational Technology (Beijing) Co., Ltd. [Jobang]
- 263. Beijing Xiaonian Cake Internet Technology Co., Ltd.
- 264. Shandong Matrix Software Engineering Co., Ltd.
- 265. Shaanxi Guoyi Software Technology Co., Ltd.
- 266. Junkai Information Technology
- 267. Village Bird Network Technology Co., Ltd.
- 268. Yunnan International Trust Co., Ltd.
- 269. Jinzhi Education
- 270. Zhuhai Nest Technology Co., Ltd.
- 271. Shanghai Yum Software Co., Ltd.
- 272. Shenzhen Kedun Technology Co., Ltd.
- 273. Hello travel [Hello]
- 274. Tuhu raises a car [Tuhu]
- 275. Cass ViewSonic Human Resources Group
- 276. Nanjing Guanwei Smart Software Technology Co., Ltd.
- 277. Hangzhou City Brain Technology Co., Ltd.
- 278. Ape tutor [Ape tutor]
- 279. Luoyang Jianchuang Network Technology Co., Ltd.
- 280. Magic ears
- 281. BOCO
- 282. Shanghai Zhaoli Technology Co., Ltd.
- 283. Sichuan Business Travel Worry-free Technology Service Co., Ltd.
- 284. UU running errands
- 285. Beijing Tiger Securities [Tiger Securities]
- 286. Youhuoshengba (Beijing) Network Technology Co., Ltd.
- 287. F5 Future Store
- 288. Shenzhen Huanyangtong Information Technology Co., Ltd.
- 289. Far EasTone Telecom
- 290. Zuoyuebang (Beijing) Education Technology Co., Ltd. [Jobbang]
- 291. Chengdu Kehong Zhixin Technology Co., Ltd.
- 292. Beijing Wooden House Times Technology Co., Ltd.
- 293. Daxuetong (Harbin) Technology Co., Ltd.
- 294. Zhejiang Huakun Daowei Data Technology Co., Ltd.
- 295. Juneyao Airlines [Juneyao Airlines]
- 296. Nanjing Yuanzhou Network Technology Co., Ltd.
- 297. Guangzhou onion omall e-commerce
- 298. Tianjin Lianwu Technology Co., Ltd.
- 299. Where to Run Technology (Beijing) Co., Ltd.
- 300. Shenzhen Meixixi Catering Co., Ltd. (Hey Tea)
- 301. Ping An Real Estate Co., Ltd. [Ping An]
- 302. Jiangsu Zhonghaisheng IoT Technology Co., Ltd.
- 303. Hunan Dentist Technology Co., Ltd.
- 304. Chongqing Civil Aviation Kaiya Information Technology Co., Ltd. (Yitonghang)
- 305. Diyi (Shanghai) Intelligent Technology Co., Ltd.
- 306. Atour
- 307. Zhejiang New Classroom Education Co., Ltd.
- 308. Beijing Fengchuang Technology Co., Ltd.
- 309. Deyi Smart City Information System Co., Ltd.
- 310. Beijing Yidian Technology Co., Ltd.
- 311. Hunan Zhishu New Dimension Information Technology Co., Ltd.
- 312. Beijing Jiuyang Bowen Culture Development Co., Ltd.
- 313. Shanghai Yuheng Information Technology Co., Ltd.
- 314.  Panorama Zhilian (Wuhan) Technology Co., Ltd.
- 315. Tianjin Yikeman International Logistics Co., Ltd.
- 316. Nanjing Aifu Road Automobile Technology Co., Ltd.
- 317. My Room Traveling Group
- 318. Zhanjiang Qinlin Technology Co., Ltd.
- 319. Shenzhen Jiangke Network Co., Ltd.
- 320. Qingdao Goodayshun Logistics Co., Ltd.
- 321. Nanjing Taichuan Information Technology Co., Ltd.
- 322. Meitu Home Technology Priority Company [Meitu]
- 323. Nanjing Taichuan Information Technology Co., Ltd.
- 324. Zhongxin Technology (Beijing) Co., Ltd.
- 325. Wuhan An'an IoT Technology Co., Ltd.
- 326. Beijing Zhike Langdao Network Technology Co., Ltd.
- 327. Shenzhen Super Orangutan Fitness Management Co., Ltd.
- 328. Chongqing Dazhi Technology Co., Ltd.
- 329. Shanghai Xiangping Information Technology Co., Ltd.
- 330. Salary paid information technology
- 331. Who to learn from?
- 332. Zhongdao (Suzhou) Tourism Network Technology Co., Ltd.
- 333. Guangzhou Xiaowei Technology Co., Ltd.
- 334. Shanghai Feima Network Technology Co., Ltd.
- 335. Tujia.com Network Technology (Beijing) Co., Ltd. [Tujia]
- 336. Guangzhou Huifan Information Technology Co., Ltd.
- 337. Tianweier Information Technology Co., Ltd.
- 338. Shanghai Jidou Technology Co., Ltd.
- 339. Suzhou Toucha Information Technology Co., Ltd.
- 340. Beijing Hot Cloud Technology Co., Ltd.
- 341. Zhongzhi Enterprise Service (Beijing) Technology Co., Ltd.
- 342. Yilian Cloud Computing (Hangzhou) Co., Ltd.
- 343. Qingdao Airlines Co., Ltd. [Qingdao Airlines]
- 344. Shanxi Boruitong Technology Co., Ltd.
- 345. Netease Hangzhou Network Co., Ltd. [Netease]
- 346. Beijing Guoguo Lexue Technology Co., Ltd.
- 347. Baiwang Co., Ltd.
- 348. China Insurance Financial Services (Shenzhen) Technology Co., Ltd.
- 349. Tianjin Yunyou Logistics Technology Co., Ltd.
- 350. Guangdong Chuangneng Technology Co., Ltd.
- 351. Shanghai Yibo Information Technology Co., Ltd.
- 352. Shenzhen Pagoda Industry (Group) Co., Ltd.
- 353. Guangzhou Fine Carved Network Technology Co., Ltd.
- 354. Wuhan Hongye Zhongchuang Technology Co., Ltd.
- 355. Jinxi Technology (Guangzhou) Co., Ltd.
- 356. Yirui International Electronic Commerce Co., Ltd.
- 357. Singularity cloud
- 358. ZOSE Information Technology Co., Ltd.
- 359. Open source project: datax-web
- 360. Yunzhisheng Intelligent Technology Co., Ltd.
- 361. Open source project: bboss
- 362. Chengdu Shenjia Technology Co., Ltd.
- 363. FunPlus [Fun Plus]
- 364. Hangzhou Chuangjiangxin Technology Co., Ltd.
- 365. Longjiang (Beijing) Technology Development Co., Ltd.
- 366. Guangzhou Yiliantong Internet Technology Co., Ltd.
- 367. Shanghai Xingai Network Technology Co., Ltd.
- 368. Hubo Network Technology (Shanghai) Co., Ltd.
- 369. Qingdao Youmi Information Technology Co., Ltd.
- 370. Baweitong Technology Co., Ltd.
- 371. Yantai Hexiang Zhixing Data Technology Co., Ltd.
- 372. Soochow Securities Co., Ltd.
- 373. Zhongtong Cloud Warehouse Co., Ltd. [Zhongtong]
- 374. Beijing Garfield Technology Co., Ltd.
- 375. Beijing Ingenuity Deduction Technology Co., Ltd.
- 376. baby walks the world
- 377. Xiamen Zhongku Technology Co., Ltd.
- 378. Haitong Securities Data Center
- 389. Hunan Happy Tongbao Small Loan Co., Ltd.
- 380. Zhejiang Dahua Technology Co., Ltd.
- 381. Hangzhou Magic Chopsticks Technology Co., Ltd.
- 382. Qingdao Zhangxuntong Blockchain Technology Co., Ltd.
- 383. Newland Financial Technology
- 384. Changzhou Xituo Software Technology Co., Ltd.
- 385. Beijing Zhengbao Grid Education Technology Co., Ltd.
- 386. Uni-President Enterprise (China) Investment Co., Ltd. [Unification]
- 387. Micro Leather Network Technology Co., Ltd.
- 388. Hangzhou Rongyisuan Technology Co., Ltd.
- 399. Qingdao Shangshaban Network Technology Co., Ltd.
- 390. Jingdong Wine World
- 391. Hangzhou Aiboshi Technology Co., Ltd.
- 392. Five Star Financial Services Holdings Limited
- 393. Fujian Lemo IoT Technology Co., Ltd.
- 394. Bailian Intelligent Technology Co., Ltd.
- 395. Shandong Energy Data Intelligence Cloud Technology Co., Ltd.
- 396. China Merchants Energy Transportation Co., Ltd.
- 397. Sany Group [Sany]
- 398. Dongbawen (Shenzhen) Health Management Co., Ltd.
- 399. Suoyi Software
- 400. Shenzhen Ningyuan Technology Co., Ltd.
- 401. Xi Niu Medical
- 402. Nanjing Zhihe Electronic Technology Co., Ltd.
- 403. Dida travel [Tick travel]
- 404. Guangzhou Huya Information Technology Co., Ltd. [Huya]
- 405. Guangzhou L'Oreal Baiku Network Technology Co., Ltd. [L'Oreal]
- 406. Weiwei Technology Co., Ltd.
- 407. I love my family Real Estate Brokerage Co., Ltd. [I love my family]
- 408. Discovery No. 9
- 409. Salary
- 410. Wuhan Krypton Cell Network Technology Co., Ltd.
- 411. Guangzhou Skechers Commercial Co., Ltd.
- 412. Weimiao Business School
- 413. Hangzhou Chesheng Technology Co., Ltd.
- 414. Shenlan Technology (Shanghai) Co., Ltd.
- 415. Anhui Zhongke Meiluo Information Technology Co., Ltd.
- 416. BYD Auto Industry Co., Ltd. [BYD]
- 417. Hunan Xiaoju Information Technology Co., Ltd.
- 418. Anhui University of Science and Technology Guochuang Software Technology Co., Ltd.
- 419. Kerry
- 420. Shaanxi Yunji Huahai Information Technology Co., Ltd.
- 421. Anhui Shenning Technology Co., Ltd.
- 422. Guangdong Kang Aiduo Digital Health Co., Ltd.
- 423. Kerry Electronic Commerce
- 424. Shanghai Times Guanghua Education Development Co., Ltd.
- 425. CityDo
- 426. Shanghai Yuzhi Information Technology Co., Ltd.
- 427. Guangdong Zhirui Technology Co., Ltd.
- 428. Xi'an Aiming Network Technology Co., Ltd.
- 429. Xinyi International Digital Medical System (Dalian) Co., Ltd.
- 430. Leqi E-Commerce
- 431. Ruida Technology
- 432. Tianjin Great Wall Binyin Auto Finance Co., Ltd.
- 433. Code Network
- 434. Dongcheng Qiaolun Software Development Studio, Dongguan City
- 435. Zhejiang Baiying Technology Co., Ltd.
- 436. Shanghai Liaidi Information Technology Co., Ltd. (Red E)
- 437. Cloud Migration Technology Co., Ltd.
- 438. Beijing Kangzhilesi Network Technology Co., Ltd. [Auntie APP]
- 439. Anhui Kaiyuan Instant Vision Technology Co., Ltd.
- 440. cubic
- 441. Xiamen Zongxing Technology
- 442. Leshan-Phoenix Semiconductor Co., Ltd.
- 443. Wuhan Optics Valley United Group Co., Ltd.
- 444. Shanghai Kingstar Software Technology Co., Ltd.
- 445. Shenzhen Yishitongda Technology Co., Ltd.
- 446. Aidong Beyond Artificial Intelligence Technology (Beijing) Co., Ltd.
- 447. Dipson (Beijing) Technology Co., Ltd.
- 448. Hand Station Technology (Beijing) Co., Ltd.
- 449. Shenzhen Huayun Zhongsheng Co., Ltd.
- 450. Shanghai Yuanquan Technology Co., Ltd.
- 451. Guangzhou Appreciation Information Technology Co., Ltd.
- 452. Amber Group
- 453. Dewei International Freight Forwarding (Shanghai) Company
- 454. Zhejiang Jeff Brothers Wisdom Technology Co., Ltd.
- 455. Xinye Technology
- 456. Kaisi Times Technology (Shenzhen) Co., Ltd.
- 457. Dalian Huaide Technology Co., Ltd.
- 458. Same Cheng Life
- 459. Pine Cone Travel
- 460. Penguin Almond Group
- 461. Ningbo Keyun Information Technology Co., Ltd.
- 462. Shanghai Grand Vios Information Technology Co., Ltd.
- 463. Hangzhou Qutao Whale Technology Co., Ltd.
- 464. Huzhou Digital Huimin Technology Co., Ltd.
- 465. Lepu (Beijing) Medical Devices Co., Ltd.
- 466. Guangzhou Qingchuan High-tech Development Co., Ltd.
- 467. Shanxi Teike Technology Co., Ltd.
- 468. Xuzhou Kasim E-Commerce Co., Ltd.
- 469. Gechuang Dongzhi Technology Co., Ltd.
- 470. Century Dragon Information Network Co., Ltd.
- 471. Bangdao Technology Co., Ltd.
- 472. Henan Zhongmeng New Cloud Technology Co., Ltd.
- 473. Hengqin Life Insurance Co., Ltd.
- 474. Shanghai Hilong Huazhong Information Technology Co., Ltd.
- 475. Shanghai Jiuzhan
- 476. Shanghai Xiandou Intelligent Robot Co., Ltd.
- 477. Guangzhou Huishang Network Technology Co., Ltd.
- 478. Shenzhen Akaso Information Co., Ltd.
- 479. Qingdao Jiajiakang Health Management Co., Ltd.
- 480. Blue City Brothers
- 481. Chengdu Tianfutong Financial Services Co., Ltd.
- 482. Shenzhen Cloud Dart Network Technology Co., Ltd.
- 483. Shanghai Film Creation Technology Co., Ltd.
- 484. Chengdu Aila IoT
- 485. Beijing Kelin Shangpin Network Technology Co., Ltd.
- 486. IT Combat Alliance
- 487. Hangzhou Yurav Technology Co., Ltd.
- 488. Zhongda Testing (Hunan) Co., Ltd.
- 489. Jiangsu Dianhu Industrial Internet Co., Ltd.
- 490. Shanghai Zhutong Information Technology Co., Ltd.
- 491. Beijing Fujie Technology Co., Ltd.
- 492. Hangzhou Yingyou Technology Co., Ltd.
- 493. Jiangsu Dianhu Industrial Internet Co., Ltd.
- 494. Shenzhen Dianmao Technology Co., Ltd.
- 495. Hangzhou Tianyin
- 496. Shenzhen Twenty-one Technology Internet Co., Ltd.
- 497. Hainan Haikou Lingdu Technology
- 498. Beijing Xiaoqu Zhipin Technology Co., Ltd.
- 499. Guangzhou Shizhu Computer Software Co., Ltd.
- 500. Shenzhen Weike Data Technology Co., Ltd.
- 501. China Medical Devices Co., Ltd.
- 502. Shanghai Yunqian Technology Co., Ltd.
- 503. Shanghai Pannong Information Technology Co., Ltd.
- 504. Guangzhou Linghang Food Co., Ltd.
- 505. Qingdao Zhangxuntong Blockchain Technology Co., Ltd.
- 506. Beijing Xinwang Digital Information Technology Co., Ltd.
- 507. Super Body Information Technology (Shenzhen) Co., Ltd.
- 508. Changsha Dianbangshou Information Technology Co., Ltd.
- 509. Shanghai Zhugong Decoration Engineering Co., Ltd.
- 510. Hangzhou Xunlian Network Technology Co., Ltd.
- 511. Chengdu Big Amoy Technology Co., Ltd.
- 512. Songguo Travel
- 513. Shenzhen City Dream Technology Co., Ltd.
- 514. SAIC Commercial Vehicle Technology Center
- 515. Beijing Aviation Information Technology Co., Ltd.
- 516. Beilong China Network (Beijing) Technology Co., Ltd.
- 517. Qianhai Super Front Desk (Shenzhen) Information Technology Co., Ltd.
- 518. Shanghai Zhongshang Network Co., Ltd.
- 519. Shanghai Zhutong Information Technology Co., Ltd.
- 520. Ningbo Juzhen Intelligent Technology Co., Ltd.
- 521. Shanghai Lingdong Digital Technology Co., Ltd.
- 522. Zhejiang Xuehai Education Technology Co., Ltd.
- 523. Juxueyun (Shandong) Information Technology Co., Ltd.
- 524. Duofluoride New Materials Co., Ltd.
- 525. Wisdom Eye Technology Co., Ltd.
- 526. Guangdong Zhitong Talent Chain Co., Ltd.
- 527. Century Kaiyuan Zhiyin Internet Technology Group Co., Ltd.
- 528. Beijing Ideal Automobile 【Ideal Automobile】
- 529. Xunyi Technology (Chongqing) Co., Ltd.
- 530. Yiwugou Electronic Commerce Co., Ltd.
- 531. Shenzhen Koradier Clothing Co., Ltd.
- 532. Jiangxi Guotai Limin Information Technology Co., Ltd.
- 533. Guangxi Radio and Television Big Data Technology Co., Ltd.
- 534. Hangzhou Aimai Technology Co., Ltd.
- 535. Guangzhou Xiaodi Technology Co., Ltd.
- 536. Jiayuan Technology Co., Ltd.
- 537. Shanghai Shenqing Information Technology Co., Ltd.
- 538. Wushang.com
- 539. Fujian Minben Information Technology Co., Ltd.
- 540. Hangzhou Huihe Information Technology Co., Ltd.
- 541. Xiamen Ailede Technology Co., Ltd.
- 542. Chengdu Fitting Future Technology Co., Ltd.
- 543. Ningbo Juzhen Intelligent Technology Co., Ltd.
- 544. Guangdong Baihui Technology Co., Ltd.
- 545. Benma Network
- 546. Shenzhen Xin'an Digital Technology Co., Ltd.
- 547. Shenzhen Sile Data Technology Co., Ltd.
- 548. Sichuan Lvyuanji Technology Co., Ltd.
- 549. Hunan Yunyi Chain Biotechnology Co., Ltd.
- 550. Hangzhou Yuancheng Technology Co., Ltd.
- 551. Beijing Kaikeba Technology Co., Ltd.
- 552. Beijing Duolaidian Information Technology Co., Ltd.
- 553. JEECG BOOT low-code development platform
- 554. Suzhou Tongyuan Soft Control Information Technology Co., Ltd.
- 555. Jiangsu Datai Information Technology Co., Ltd.
- 556. Beijing Dayu Huizhi
- 557. Beijing Shengzhe Technology Co., Ltd.
- 558. Guangzhou Titan Technology Co., Ltd.
- 559. Beijing Dayu Huizhi Technology Co., Ltd.
- 560. Hunan Dinghan Culture Co., Ltd.
- 561. Suzhou Anruan Information Technology Co., Ltd.
- 562. mango tv
- 563. Shanghai Yisaiqi Software Co., Ltd.
- 564. Zhongying Youchuang Information Technology Co., Ltd.
- 565. Lehu Apartment
- 566. Qiming Information
- 567. Suzhou Anruan
- 568. Nanjing Fujin Software Technology Co., Ltd.
- 569. Shenzhen Xinke Polymerization Network Technology Co., Ltd.
- 570. Hello Now (Beijing) Technology Co., Ltd.
- 571. 360 exam book
- 572. Beijing One Zero Technology Co., Ltd.
- 573. Xiamen Xingzong Information
- 574. Dalligent Solusi Indonesia
- 575. Shenzhen Huapu IoT Technology Co., Ltd.
- 576. Shenzhen Xingjian Automation Co., Ltd.
- 577. Shenzhen Furong Information Technology Service Co., Ltd.
- 578. Blue Bird Cloud
- 579. Shanghai Pengbo Financial Information Co., Ltd.
- 580. Beijing Xiaoya Technology Co., Ltd.
- 581. Hangzhou Yingquan Cloud Technology Co., Ltd.
- 582. Weike data
- 583. GOSO Sweet Honey Girlfriend
- 584. Puleshi (Shanghai) Digital Technology Co., Ltd.
- 585. Network Technology Department of Kabeitang, Yanta District, Xi'an City
- 586. Ningbo Juzhen Intelligent Technology Co., Ltd.
- 587. Puleshi Digital Technology Co., Ltd.
- 588. Jiangsu Crab Network Technology Co., Ltd.
- 589. Hangzhou Weizhi Technology Co., Ltd.
- 590. Anji Zhixing Logistics Co., Ltd.
- 591. Watson Home Furnishing Group Co., Ltd.
- 592. Maxim's Food (Guangzhou) Co., Ltd.
- 593. Huolala [Huolala APP]
- 594. Hangzhou Si Tao Rui Technology Co., Ltd.
- 595. Hangzhou Jiurong Technology Co., Ltd.
- 596. Beijing Youhai Network Technology Co., Ltd.
- 597. Zhejiang Dawei High-tech Co., Ltd.
- 598. Guangdong-Hong Kong-Macao Greater Bay Area Digital Economy Research Institute
- 599. Pukang (Hangzhou) Health Technology Co., Ltd.
- 600. Huaxi Securities Co., Ltd. [Huaxi Securities]
- 601. Hangzhou Hikvision Robot Co., Ltd. [Hikvision]
- 602. Henan Chenbang Information Technology Co., Ltd.
- 603. Chengdu Dimension Node Network Technology Co., Ltd.
-...

> For more connected companies, welcome to register at [registration address](https://github.com/xuxueli/xxl-job/issues/1 ), registration is only for product promotion.

Welcome everyone's attention and use, XXL-JOB will also embrace changes and continue to develop.


### 1.5 Download

#### Document address

- [Chinese document](https://www.xuxueli.com/xxl-job/)
- [English Documentation](https://www.xuxueli.com/xxl-job/en/)

#### Source warehouse address

Source Code Warehouse Address | Release Download
--- | ---
[https://github.com/xuxueli/xxl-job](https://github.com/xuxueli/xxl-job) | [Download](https://github.com/xuxueli/xxl-job/releases )
[http://gitee.com/xuxueli0323/xxl-job](http://gitee.com/xuxueli0323/xxl-job) | [Download](http://gitee.com/xuxueli0323/xxl-job/releases )


#### Central warehouse address

```
<!-- http://repo1.maven.org/maven2/com/xuxueli/xxl-job-core/ -->
<dependency>
     <groupId>com.xuxueli</groupId>
     <artifactId>xxl-job-core</artifactId>
     <version>${latest stable version}</version>
</dependency>
```


### 1.6 Environment
-Maven3+
-Jdk1.8+
-Mysql5.7+

## 2. Quick start

### 2.1 Initialize "Scheduling Database"
Please download the project source code and unzip it, get the "Scheduling Database Initialization SQL Script" and execute it.

The location of "Scheduling Database Initialization SQL Script" is:

     /xxl-job/doc/db/tables_xxl_job.sql

The dispatch center supports cluster deployment, and each node must be connected to the same mysql instance in the case of a cluster;

If mysql is the master-slave, the dispatch center cluster node must force the master library;

### 2.2 Compile the source code
Unzip the source code, import the source code into the IDE according to the maven format, and compile it with maven. The source code structure is as follows:

     xxl-job-admin: scheduling center
     xxl-job-core: public dependencies
     xxl-job-executor-samples: Executor Sample (select the appropriate version of the executor, which can be used directly, or refer to it and transform the existing project into an executor)
         :xxl-job-executor-sample-springboot: Springboot version, manage the executor through Springboot, this method is recommended;
         :xxl-job-executor-sample-frameless: frameless version;
        

### 2.3 Configuring and deploying "dispatch center"

     Dispatch center project: xxl-job-admin
     Role: Unified management of scheduling tasks on the task scheduling platform, responsible for triggering scheduling execution, and providing a task management platform.

#### Step 1: Dispatch center configuration:
Address of dispatch center configuration file:

     /xxl-job/xxl-job-admin/src/main/resources/application.properties


Description of dispatch center configuration content:

     ### Dispatch center JDBC link: Please keep the link address consistent with the address of the dispatch database created in Chapter 2.1
     spring.datasource.url=jdbc:mysql://127.0.0.1:3306/xxl_job?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai
     spring.datasource.username=root
     spring.datasource.password=root_pwd
     spring.datasource.driver-class-name=com.mysql.jdbc.Driver
    
     ### Alarm email
     spring.mail.host=smtp.qq.com
     spring.mail.port=25
     spring.mail.username=xxx@qq.com
     spring.mail.password=xxx
     spring.mail.properties.mail.smtp.auth=true
     spring.mail.properties.mail.smtp.starttls.enable=true
     spring.mail.properties.mail.smtp.starttls.required=true
     spring.mail.properties.mail.smtp.socketFactory.class=javax.net.ssl.SSLSocketFactory
    
     ### Dispatch Center Communication TOKEN [Optional]: enable when not empty;
     xxl.job.accessToken=
    
     ### Dispatch Center Internationalization Configuration [Required]: The default is "zh_CN"/Simplified Chinese, the optional range is "zh_CN"/Simplified Chinese, "zh_TC"/Traditional Chinese and "en"/English;
     xxl.job.i18n=zh_CN
    
     ## Scheduling thread pool maximum thread configuration [required]
     xxl.job.triggerpool.fast.max=200
     xxl.job.triggerpool.slow.max=100
    
     ### The number of days to save the log table data in the dispatching center [Required]: Automatic cleaning of expired logs; it will take effect when the limit is greater than or equal to 7, otherwise, such as -1, turn off the automatic cleaning function;
     xxl.job.log retentiondays=30
    
    

#### Step 2: Deploy the project:
If the above configuration has been done correctly, the project can be compiled, packaged and deployed.

Dispatch center access address: http://localhost:8080/xxl-job-admin (this address will be used by the executor as the callback address)

The default login account is "admin/123456". After login, the running interface is as shown in the figure below.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_6yC0.png "Enter picture title here")

So far the "dispatch center" project has been deployed successfully.

#### Step 3: Dispatch center cluster (optional):
The dispatch center supports cluster deployment to improve the disaster recovery and availability of the dispatch system.

When deploying a dispatch center cluster, there are several requirements and suggestions:
- DB configuration remains consistent;
- The clocks of the cluster machines are consistent (neglected by the stand-alone cluster);
- Suggestion: It is recommended to use nginx to do load balancing for the dispatch center cluster and assign domain names. Operations such as scheduling center access, executor callback configuration, and calling API services are all performed through this domain name.


#### Others: Docker image way to build dispatching center:

- Download mirror

```
// Docker address: https://hub.docker.com/r/xuxueli/xxl-job-admin/ (it is recommended to specify the version number)
docker pull xuxueli/xxl-job-admin
```

- create container and run

```
docker run -p 8080:8080 -v /tmp:/data/applogs --name xxl-job-admin -d xuxueli/xxl-job-admin:{specified version}

/**
* If you need to customize mysql and other configurations, you can specify it through "-e PARAMS", and the parameter format is PARAMS="--key=value --key2=value2";
* Configuration item reference file: /xxl-job/xxl-job-admin/src/main/resources/application.properties
* If you need to customize JVM memory parameters and other configurations, you can specify it through "-e JAVA_OPTS", and the parameter format is JAVA_OPTS="-Xmx512m";
*/
docker run -e PARAMS="--spring.datasource.url=jdbc:mysql://127.0.0.1:3306/xxl_job?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai" -p 8080:8080 -v /tmp:/data/applogs --name xxl-job-admin -d xuxueli/xxl-job-admin:{specified version}
```


### 2.4 Configure and deploy "executor project"

     "Executor" project: xxl-job-executor-sample-springboot (multiple versions of executors are available, now take the springboot version as an example, which can be used directly, or refer to it and transform existing projects into executors)
     Role: Responsible for receiving and executing the scheduling of the "dispatch center"; the executor can be directly deployed or integrated into existing business projects.
    
#### Step 1: maven dependency
Confirm that the maven dependency of "xxl-job-core" is introduced into the pom file;
    
#### Step 2: Executor configuration
Actuator configuration, configuration file address:

     /xxl-job/xxl-job-executor-samples/xxl-job-executor-sample-springboot/src/main/resources/application.properties

Actuator configuration, configuration description:

     ### Dispatch center deployment root address [optional]: If there are multiple addresses for dispatch center cluster deployment, separate them with commas. The executor will use this address for "executor heartbeat registration" and "task result callback"; if it is empty, automatic registration will be turned off;
     xxl.job.admin.addresses=http://127.0.0.1:8080/xxl-job-admin
    
     ### Actuator communication token [Optional]: enable when not empty;
     xxl.job.accessToken=
    
     ### Actuator AppName [Optional]: Actuator heartbeat registration group basis; if it is empty, automatic registration will be turned off
     xxl.job.executor.appname=xxl-job-executor-sample
     ### Executor Registration [Optional]: Use this configuration as the registration address first, and use the embedded service "IP:PORT" as the registration address when it is empty. In this way, it supports the dynamic IP and dynamic mapping port issues of container type executors more flexibly.
     xxl.job.executor.address=
     ### Executor IP [Optional]: The default is empty, which means that the IP is automatically obtained. When there are multiple network cards, the specified IP can be manually set. The IP will not be bound to the Host and is only used for communication; the address information is used for "executor registration" and "The dispatch center requests and triggers the task";
     xxl.job.executor.ip=
     ### Actuator port number [Optional]: If it is less than or equal to 0, it will be obtained automatically; the default port is 9999. When deploying multiple executors on a single machine, be careful to configure different executor ports;
     xxl.job.executor.port=9999
     ### Executor running log file storage disk path [optional]: You need to have read and write permissions for this path; if it is empty, use the default path;
     xxl.job.executor.logpath=/data/applogs/xxl-job/jobhandler
     ### Executor log file storage days [Optional]: expired logs are automatically cleaned up, and the limit value is greater than or equal to 3. Otherwise, such as -1, the automatic cleaning function is turned off;
     xxl.job.executor.log retention days=30
    

#### Step 3: Actuator component configuration

Actuator component, configuration file address:

     /xxl-job/xxl-job-executor-samples/xxl-job-executor-sample-springboot/src/main/java/com/xxl/job/executor/core/config/XxlJobConfig.java

Actuator components, configuration description:

```
@Bean
public XxlJobSpringExecutor xxlJobExecutor() {
     logger.info(">>>>>>>>>>>> xxl-job config init.");
     XxlJobSpringExecutor xxlJobSpringExecutor = new XxlJobSpringExecutor();
     xxlJobSpringExecutor.setAdminAddresses(adminAddresses);
     xxlJobSpringExecutor.setAppname(appname);
     xxlJobSpringExecutor.setIp(ip);
     xxlJobSpringExecutor.setPort(port);
     xxlJobSpringExecutor.setAccessToken(accessToken);
     xxlJobSpringExecutor.setLogPath(logPath);
     xxlJobSpringExecutor.setLogRetentionDays(logRetentionDays);

     return xxlJobSpringExecutor;
}
```

#### Step 4: Deploy the executor project:
If the above configurations have been performed correctly, the executor project can be compiled and deployed. The system provides a variety of executor Sample sample projects. Just choose one of them. The respective deployment methods are as follows.

     xxl-job-executor-sample-springboot: The project is compiled and packaged into an executable JAR package of springboot type, and the command can be started;
     xxl-job-executor-sample-frameless: The project is compiled and packaged into a JAR package, and the command can be started;
    

So far the "Actuator" project has been deployed.

#### Step 5: Executor cluster (optional):
The executor supports cluster deployment, improves the availability of the scheduling system, and improves task processing capabilities.

When deploying executor clusters, there are several requirements and suggestions:
- The executor callback address (xxl.job.admin.addresses) needs to be consistent; the executor performs operations such as executor automatic registration according to this configuration.
- The AppName (xxl.job.executor.appname) in the same executor cluster needs to be consistent; the scheduling center dynamically discovers the online executor lists of different clusters according to this configuration.


### 2.5 Develop the first task "Hello World"
This example takes creating a task in the "GLUE mode (Java)" operation mode as an example. For more detailed configuration of tasks, please refer to "Chapter 3: Detailed Explanation of Tasks".
(The execution code of "GLUE mode (Java)" is hosted to the dispatch center for online maintenance, which is simpler and lighter than the "Bean mode task" that needs to be developed and deployed in the executor project.)

> Prerequisite: Please confirm that the "dispatch center" and "actuator" projects have been successfully deployed and started;

#### Step 1: Create a new task:
Log in to the dispatch center and click the "New Task" button as shown in the figure below to create a new sample task. Then, refer to the parameter configuration of the task in the screenshot below, and click Save.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_o8HQ.png "Enter picture title here")

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_ZAsz.png "Enter picture title here")


#### Step 2: "GLUE mode (Java)" task development:
Please click the "GLUE" button on the right side of the task to enter the "GLUE editor development interface", as shown in the figure below. The task in the "GLUE mode (Java)" running mode has initialized the sample task code by default, that is, printing Hello World.
(The "GLUE mode (Java)" operation mode task is actually a piece of Java class code inherited from IJobHandler. It runs in the executor project and can use @Resource/@Autowire to inject other services in the executor. Details Please see Chapter 3)

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_Fgql.png "Enter picture title here")

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_dNUJ.png "Enter picture title here")

#### Step 3: Trigger execution:
Please click the "Execute" button on the right side of the task to manually trigger a task execution (usually, the task scheduling is triggered by configuring a Cron expression).

#### Step 4: Check the log:
Please click the "Log" button on the right side of the task to go to the task log interface to view the task log.
In the task log interface, you can view the historical scheduling records of the task, as well as the task scheduling information, execution parameters and execution information of each scheduling. Click the "Execution Log" button on the right side of the running task to enter the log console to view the real-time execution log.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_inc8.png "Enter picture title here")

In the log console, you can view the log information output by the task running on the executor side in real time in Rolling mode, and monitor the progress of the task in real time;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_eYrv.png "Enter picture title here")

## 3. task details

### Configuration property details:

     Basic configuration:
         - Executor: The executor bound to the task. When the task is triggered and scheduled, it will automatically discover the registered executor, realizing the task automatic discovery function; on the other hand, it is also convenient to group tasks. Each task must be bound to an executor, which can be set in "Executor Management";
         - Task description: the description information of the task, which is convenient for task management;
         - Person in charge: the person in charge of the task;
         - Alarm email: email address for email notification when task scheduling fails, supports configuration of multiple email addresses, and separates multiple email addresses with commas;
        
     Trigger configuration:
         - Scheduling type:
             None: This type will not actively trigger scheduling;
             CRON: This type will trigger task scheduling through CRON;
             Fixed speed: This type will trigger task scheduling at a fixed speed; it will be triggered periodically at a fixed interval;
             Fixed delay: This type will trigger task scheduling with a fixed delay; according to the fixed delay time, the delay time will be calculated from the end of the last scheduling, and the next scheduling will be triggered after the delay time is reached;
         - CRON: Cron expression that triggers task execution;
         - Fixed speed: the time interval of fixed speed, in seconds;
         - Fixed delay: the time interval of the fixed delay, in seconds;
        
     Task configuration:
         - Operating mode:
             BEAN mode: tasks are maintained on the executor side in the form of JobHandler; it needs to be combined with the "JobHandler" attribute to match the tasks in the executor;
             GLUE mode (Java): The task is maintained in the dispatch center in source code; the task in this mode is actually a piece of Java class code inherited from IJobHandler and maintained in "groovy" source code. It runs in the executor project and can be used @Resource /@Autowire injects other services in the executor;
             GLUE mode (Shell): The task is maintained in the dispatch center in source code; the task in this mode is actually a "shell" script;
             GLUE mode (Python): the task is maintained in the dispatch center as source code; the task in this mode is actually a "python" script;
             GLUE mode (PHP): The task is maintained in the dispatch center in the form of source code; the task in this mode is actually a "php" script;
             GLUE mode (NodeJS): the task is maintained in the dispatch center in the form of source code; the task in this mode is actually a "nodejs" script;
             GLUE mode (PowerShell): The task is maintained in the dispatch center as source code; the task in this mode is actually a "PowerShell" script;
         - JobHandler: It takes effect when the operating mode is "BEAN mode", corresponding to the newly developed JobHandler class "@JobHandler" annotation custom value value in the executor;
         - Execution parameters: parameters required for task execution;
        
     Advanced configuration:
         - Routing strategy: When the executor cluster is deployed, rich routing strategies are provided, including;
             FIRST (the first): fixedly select the first machine;
             LAST (last one): fixedly select the last machine;
             ROUND:;
             RANDOM (random): random selection of online machines;
             CONSISTENT_HASH (consistency HASH): Each task selects a certain machine according to the Hash algorithm, and all tasks are evenly hashed on different machines.
             LEAST_FREQUENTLY_USED (least frequently used): The machine with the lowest frequency of use is elected first;
             LEAST_RECENTLY_USED (most recently unused): the machine that has not been used for the longest time will be elected first;
             FAILOVER (failover): Carry out heartbeat detection in sequence, and the first machine with successful heartbeat detection is selected as the target executor and initiates scheduling;
             BUSYOVER (busy transfer): The idle detection is performed sequentially, and the first machine with a successful idle detection is selected as the target executor and initiates scheduling;
             SHARDING_BROADCAST (fragmentation broadcast): Broadcast triggers all machines in the corresponding cluster to execute a task, and the system automatically transmits fragmentation parameters; fragmentation tasks can be developed according to fragmentation parameters;
         - Subtask: Each task has a unique task ID (the task ID can be obtained from the task list). When the execution of this task is completed and executed successfully, an active scheduling of the task corresponding to the subtask ID will be triggered.
         - Scheduling expiration policy:
             - Ignore: After the schedule expires, ignore the expired task and recalculate the next trigger time from the current time;
             - Execute once immediately: After the schedule expires, execute once immediately, and recalculate the next trigger time from the current time;
         - Blocking processing strategy: the processing strategy when the scheduling is too intensive for the executor to process in time;
             Stand-alone serial (default): After the scheduling request enters the single-machine executor, the scheduling request enters the FIFO queue and runs in serial mode;
             Discard subsequent scheduling: After the scheduling request enters the stand-alone executor, it is found that the executor has a running scheduling task, and this request will be discarded and marked as failed;
             Scheduling before coverage: After the scheduling request enters the stand-alone executor, if the executor finds that there is a running scheduling task, it will terminate the running scheduling task and clear the queue, and then run the local scheduling task;
         - Task timeout: Support custom task timeout, task running timeout will actively interrupt the task;
         - Number of failed retries; supports customizing the number of failed retries of a task, and when a task fails, it will actively retry according to the preset number of failed retries;
    
    
    

    
### 3.1 BEAN mode (class form)

Bean mode tasks support class-based development, and each task corresponds to a Java class.

- Advantages: No restrictions on the project environment, good compatibility. Even frameless projects, such as projects directly started by the main method, can also provide support, you can refer to the sample project "xxl-job-executor-sample-frameless";
- shortcoming:
     - Each task needs to occupy a Java class, resulting in a waste of classes;
     - Does not support automatic scanning of tasks and injection into the executor container, manual injection is required.

#### Step 1: In the executor project, develop the Job class:

     1. Develop a JobHandler class inherited from "com.xxl.job.core.handler.IJobHandler" to implement the task method.
     2. Manually inject it into the executor container as follows.
     ```
     XxlJobExecutor.registJobHandler("demoJobHandler", new DemoJobHandler());
     ```

#### Step 2: Scheduling center, create a new scheduling task
Subsequent steps are consistent with "3.2 BEAN Mode (Method Form)", you can refer to it.


### 3.2 BEAN mode (method form)

The Bean mode task supports the method-based development method, and each task corresponds to a method.

- advantage:
     - Each task only needs to develop one method and add "@XxlJob" annotation, which is more convenient and faster.
     - Supports automatic scanning of tasks and injection into the executor container.
- Disadvantage: Spring container environment is required;

> For method-based development tasks, the bottom layer will generate a JobHandler proxy. Like the class-based method, tasks will also exist in the executor task container in the form of JobHandler.

#### Step 1: In the executor project, develop the Job method:

     1. Task development: In the Spring Bean instance, develop the Job method;
     2. Annotation configuration: add the annotation "@XxlJob(value="custom jobhandler name", init = "JobHandler initialization method", destroy = "JobHandler destruction method")" to the Job method, and the annotation value value corresponds to the newly created dispatching center The value of the job's JobHandler property.
     3. Execution log: You need to print the execution log through "XxlJobHelper.log";
     4. Task result: The default task result is "success" and does not need to be actively set; if you have a request, such as setting the task result to fail, you can set the task result independently through "XxlJobHelper.handleFail/handleSuccess";
    
```
// Refer to "com.xxl.job.executor.service.jobhandler.SampleXxlJob" in the Sample Executor, as follows:
@XxlJob("demoJobHandler")
public void demoJobHandler() throws Exception {
     XxlJobHelper.log("XXL-JOB, Hello World.");
}
```

#### Step 2: Scheduling center, create a new scheduling task
Refer to the above "Detailed Description of Configuration Properties" to configure the parameters of the newly created task, select "BEAN mode" as the running mode, and fill in the value defined in the task annotation "@XxlJob" for the JobHandler property;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_ZAsz.png "Enter picture title here")

#### Native built-in Bean mode task
For the convenience of user reference and quick practicality, the example executor provides multiple Bean mode task handlers natively, which can be directly configured and practical, as follows:

- demoJobHandler: a simple sample task, which simulates time-consuming task logic inside the task, and users can experience functions such as Rolling Log online;
- shardingJobHandler: sharding example task, which simulates and processes sharding parameters inside the task, please refer to Familiar with sharding tasks;
- httpJobHandler: General HTTP task handler; the business side only needs to provide information such as HTTP links, and there are no restrictions on languages and platforms. The input parameters of the sample task are as follows:
     ```
     url: http://www.xxx.com
     method: get or post
     data: post-data
     ```
- commandJobHandler: general command line task handler; the business side only needs to provide the command line; such as the "pwd" command;


### 3.3 GLUE mode (Java)
The task is maintained in the dispatch center in the form of source code, supports online update through the Web IDE, and compiles and takes effect in real time, so there is no need to specify a JobHandler. The development process is as follows:

#### Step 1: Scheduling center, create a new scheduling task:
Refer to the "Detailed Description of Configuration Properties" above to configure the parameters of the newly created task, and select "GLUE Mode (Java)" as the operating mode;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_tJOq.png "Enter picture title here")

#### Step 2: Develop task code:
Select the specified task, click the "GLUE" button on the right side of the task, and you will go to the Web IDE interface of the GLUE task, which supports the development of the task code (you can also copy and paste it into the editor after the development is completed in the IDE).

Version backtracking function (version backtracking of 30 versions is supported): On the Web IDE interface of the GLUE task, select the drop-down box "Version Backtracking" in the upper right corner, and the update history of the GLUE will be listed. Select the corresponding version to display the version code. After saving, the GLUE code will roll back to the corresponding historical version;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_dNUJ.png "Enter picture title here")

### 3.4 GLUE mode (Shell)

#### Step 1: Scheduling center, create a new scheduling task
Refer to the "Detailed Description of Configuration Properties" above to configure the parameters of the newly created task, and select "GLUE Mode (Shell)" as the operating mode;

#### Step 2: Develop task code:
Select the specified task, click the "GLUE" button on the right side of the task, and you will go to the Web IDE interface of the GLUE task, which supports the development of the task code (you can also copy and paste it into the editor after the development is completed in the IDE).

The mode's task is actually a "shell" script;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_iUw0.png "Enter picture title here")

### 3.4 GLUE mode (Python)

#### Step 1: Scheduling center, create a new scheduling task
Refer to the above "Detailed Description of Configuration Properties" to configure the parameters of the newly created task, and select "GLUE Mode (Python)" as the operating mode;

#### Step 2: Develop task code:
Select the specified task, click the "GLUE" button on the right side of the task, and you will go to the Web IDE interface of the GLUE task, which supports the development of the task code (you can also copy and paste it into the editor after the development is completed in the IDE).

A task for this mode is actually a "python" script;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_BPLG.png "Enter picture title here")

### 3.5 GLUE mode (NodeJS)

#### Step 1: Scheduling center, create a new scheduling task
Refer to the above "Detailed Description of Configuration Properties" to configure the parameters of the newly created task, and select "GLUE Mode (NodeJS)" as the operating mode;

#### Step 2: Develop task code:
Select the specified task, click the "GLUE" button on the right side of the task, and you will go to the Web IDE interface of the GLUE task, which supports the development of the task code (you can also copy and paste it into the editor after the development is completed in the IDE).

The mode's task is actually a "nodeJS" script;

### 3.6 GLUE mode (PHP)
ditto

### 3.7 GLUE mode (PowerShell)
ditto

## 4. Operation Guide

### 4.1 Configure Actuator
Click to enter the "Executor Management" interface, as shown in the figure below:
![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_Hr2T.png "Enter picture title here")

     1. "Scheduling Center OnLine:" displays the online "Scheduling Center" list on the right side. After the task is executed, it will call back the dispatching center in failover mode to notify the execution result, avoiding the single-point risk of callback;
     2. The online executor list is displayed in the "Executor List", and the cluster machine corresponding to the executor can be viewed through "OnLine Machine".

Click the button "+ Add Actuator" and the pop-up box is as shown in the figure below, you can add an actuator configuration:

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_V3vF.png "Enter picture title here")

Actuator property description

     AppName: AppName is the unique identifier of each executor cluster, and the executor will periodically register automatically with AppName as the object. Through this configuration, the registered executors can be automatically discovered for use in task scheduling;
     Name: The name of the executor, because the AppName is limited to letters and numbers, the readability is not strong, the name is to improve the readability of the executor;
     Sorting: The sorting of executors, where executors are needed in the system, if a task is added, the list of available executors will be read according to this sorting;
     Registration method: the way the dispatch center obtains the address of the executor;
         Automatic registration: The executor automatically registers the executor, and the dispatch center can dynamically discover the machine address of the executor through the underlying registry;
         Manual entry: manually enter the address information of the actuator, and separate multiple addresses with commas for use by the dispatch center;
     Machine address: it is valid when the "registration method" is "manual input", and supports manual maintenance of the address information of the actuator;

### 4.2 Create a new task
Enter the task management interface, click the "Add Task" button, configure the task properties in the pop-up "Add Task" interface and save it. For the details page, refer to the chapter "3. Detailed Task Explanation".

### 4.3 Edit task
Enter the task management interface, select the specified task. Click the "Edit" button on the right side of the task, update the task properties in the pop-up "Edit Task" interface and save it. You can modify the set task property information:

### 4.4 Edit GLUE code

This operation is only for GLUE tasks.

Select the specified task and click the "GLUE" button on the right side of the task to go to the Web IDE interface of the GLUE task, which supports the development of the task code. Refer to chapter "3.3 GLUE Mode (Java)".

### 4.5 Start/stop tasks
Tasks can be "started" and "stopped".
It should be noted that the start/stop here is only for the subsequent scheduling trigger behavior of the task, and will not affect the scheduled tasks that have already been triggered. If you need to terminate the scheduled tasks that have been triggered, please refer to "4.9 Terminate Running Tasks"

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_ZAhX.png "Enter picture title here")

### 4.6 Manually trigger a schedule
Click the "Execute" button to manually trigger a task scheduling without affecting the original scheduling rules.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_ZAhX.png "Enter picture title here")

### 4.7 View scheduling log
Click the "Log" button to view the task history scheduling log. On the history transfer log interface, you can view the scheduling results and execution results of each task scheduling, and click the "Execution Log" button to view the complete log of the executor.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_ZAhX.png "Enter picture title here")

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_UDSo.png "Enter picture title here")

     Scheduling time: the time when the "scheduling center" triggers this scheduling and sends a task execution signal to the "executor";
     Scheduling result: "Scheduling Center" triggers the result of this scheduling, 200 means success, 500 or other means failure;
     Scheduling Remarks: "Scheduling Center" triggers the log information of this scheduling;
     Executor address: the address of the machine to execute this task
     Running mode: The running mode of the task when scheduling is triggered. For the running mode, please refer to the chapter "3. Task details";
     Task parameters: input parameters for local task execution
     Execution time: the callback time after the execution of this task in the "Executor";
     Execution result: the result of this task execution in the "Executor", 200 means success, 500 or other means failure;
     Execution remarks: the log information of this task execution in the "Executor";
     operate:
         "Execution Log" button: click to view detailed log information of local task execution; see "4.8 View Execution Log" for details;
         "Terminate task" button: Click to terminate the execution thread of this task on the corresponding executor of local scheduling, including unexecuted blocked tasks;

### 4.8 View execution log
Click the "Execution Log" button on the right side of the execution log to jump to the execution log interface, where you can view the complete log printed in the business code, as shown in the figure below;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_tvGI.png "Enter picture title here")

### 4.9 Terminate running tasks
Only for executing tasks.
On the task log interface, click the "Terminate Task" button on the right, and a task termination request will be sent to the executor corresponding to this task, and this task will be terminated, and the entire task execution queue will be cleared at the same time.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_hIci.png "Enter picture title here")

When the task is terminated by "interrupting" the thread of execution, an "InterruptedException" will be thrown. Therefore, if the exception is caught and digested inside the JobHandler, the task termination function will not be available.

Therefore, if the above-mentioned task termination is unavailable, it is necessary to perform special handling (throwing upward) for the "InterruptedException" exception in the JobHandler. The correct logic is as follows:
```
try {
     // do something
} catch (Exception e) {
     if (e instanceof InterruptedException) {
         throw e;
     }
     logger. warn("{}", e);
}
```

Moreover, when the child thread is started in the JobHandler, the child thread cannot catch and handle "InterruptedException", and should actively throw it upward.

When the task terminates, the "destroy()" method corresponding to the JobHandler will be executed, which can be used to handle some resource recovery logic.


### 4.10 Delete execution log
In the task log interface, after selecting the executor and task, click the "Delete" button on the right, and a "Log Cleanup" pop-up box will appear. The pop-up box supports the selection of different types of log cleanup strategies. After selecting it, click the "OK" button. Can perform log cleanup operations;
![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_Ypik.png "Enter picture title here")

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_EB65.png "Enter picture title here")

### 4.11 Delete task
Click the Delete button to delete the corresponding task.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_Z9Qr.png "Enter picture title here")

### 4.12 User Management
Enter the "User Management" interface to view and manage user information;

Currently users are divided into two roles:
- Administrator: has full authority, supports online management of user information, assigns authority to users, and the granularity of authority allocation is executor;
- Ordinary users: only have the executors assigned permissions, and the operation permissions of related tasks;

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_1001.png "Enter picture title here")

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_1002.png "Enter picture title here")


## 5. the overall design
### 5.1 Source directory introduction
     - /doc : documentation
     - /db : "Scheduling database" table creation script
     - /xxl-job-admin : scheduling center, project source code
     - /xxl-job-core : Public Jar dependencies
     - /xxl-job-executor-samples : Executor, Sample sample project (you can develop on this project, or transform existing projects into executor projects)

### 5.2 "Scheduling database" configuration
The XXL-JOB scheduling module is based on self-developed scheduling components and supports cluster deployment. The scheduling database table is described as follows:

     - xxl_job_lock: task scheduling lock table;
     - xxl_job_group: executor information table, maintain task executor information;
     - xxl_job_info: Scheduling extension information table: used to save the extended information of XXL-JOB scheduling tasks, such as task grouping, task name, machine address, executor, execution input parameters and alarm emails, etc.;
     - xxl_job_log: Scheduling log table: used to save the historical information of XXL-JOB task scheduling, such as scheduling results, execution results, scheduling input parameters, scheduling machines and executors, etc.;
     - xxl_job_log_report: Scheduling log report: The user stores the report of XXL-JOB task scheduling log, which will be used in the report function page of the dispatching center;
     - xxl_job_logglue: task GLUE log: used to save GLUE update history, used to support GLUE version backtracking function;
     - xxl_job_registry: executor registry, which maintains online executor and dispatch center machine address information;
     - xxl_job_user: system user table;


### 5.3 Architecture Design
#### 5.3.1 Design thinking
The dispatching behavior is abstracted into a public platform of "dispatching center", and the platform itself does not undertake business logic, and the "dispatching center" is responsible for initiating dispatching requests.

The tasks are abstracted into scattered JobHandlers, which are managed by the "executor", and the "executor" is responsible for receiving scheduling requests and executing the business logic in the corresponding JobHandler.

Therefore, the two parts of "scheduling" and "task" can be decoupled from each other to improve the overall stability and scalability of the system;

#### 5.3.2 System composition
- **Scheduling Module (Scheduling Center)**:
     Responsible for managing scheduling information, sending scheduling requests according to scheduling configuration, and not responsible for business codes. The scheduling system is decoupled from tasks, which improves system availability and stability, and at the same time, the performance of the scheduling system is no longer limited by task modules;
     Support visual, simple and dynamic management scheduling information, including task creation, update, deletion, GLUE development and task alarm, etc. All the above operations will take effect in real time, and support monitoring scheduling results and execution logs, and support executor failover.
- **execution module (actuator)**:
     Responsible for receiving scheduling requests and executing task logic. The task module focuses on operations such as task execution, making development and maintenance easier and more efficient;
     Receive execution requests, termination requests, log requests, etc. from the "scheduling center".

#### 5.3.3 Architecture Diagram

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_Qohm.png "Enter picture title here")

### 5.4 Scheduling module analysis
#### 5.4.1 Insufficiency of quartz
As the leader in open source job scheduling, Quartz is the first choice for job scheduling. However, in the cluster environment, Quartz uses API to manage tasks, so as to avoid the above problems, but there are also the following problems:
   
- Problem 1: The method of calling the API to operate the task is not humanized;
- Question 2: It is necessary to persist the business QuartzJobBean to the underlying data table, and the system is quite intrusive.
- Question 3: The scheduling logic and QuartzJobBean are coupled in the same project, which will lead to a problem. When the number of scheduling tasks is gradually increasing, and the scheduling task logic is gradually aggravating, the performance of the scheduling system will be greatly limited by the business. ;
- Question 4: The underlying layer of quartz acquires DB locks in a "preemptive" manner and the successful preemptive nodes are responsible for running tasks, which will lead to a very large disparity in node load; while XXL-JOB implements "coordinated distribution" running tasks through executors to give full play to the cluster The advantage is that the load is balanced on each node.

XXL-JOB makes up for the above shortcomings of quartz.

#### 5.4.2 Self-developed scheduling module
XXL-JOB finally chose the self-developed scheduling component (the early scheduling component was based on Quartz); on the one hand, it is to simplify the system and reduce redundant dependencies; on the other hand, it is to provide the controllability and stability of the system;

The "scheduling module" and "task module" in XXL-JOB are completely decoupled. When the scheduling module performs task scheduling, it will analyze different task parameters and initiate remote calls to invoke their respective remote executor services. This invocation model is similar to RPC invocation. The dispatch center provides the function of invoking the agent, while the executor provides the function of remote service.

#### 5.4.3 Dispatch center HA (cluster)
The database-based cluster solution uses Mysql as the database; when scheduled tasks are scheduled in a cluster distributed concurrent environment, tasks will be reported on each node and stored in the database, and the trigger will be taken out from the database to execute during execution. If the name and execution time are the same, there is only one node to execute this task.

#### 5.4.4 Scheduling thread pool
Scheduling is implemented in a thread pool to avoid task scheduling delays caused by single-thread blocking.

#### 5.4.5 Parallel Scheduling
The XXL-JOB scheduling module adopts a parallel mechanism by default. In the case of multi-thread scheduling, the probability of the scheduling module being blocked is very low, which greatly improves the load capacity of the scheduling system.

Different tasks of XXL-JOB are scheduled and executed in parallel.
A single task of XXL-JOB runs in parallel for multiple executors, and executes serially for a single executor. Also supports task termination.

#### 5.4.6 Expiration processing strategy
Processing strategy when task scheduling misses the trigger time:
- Possible reasons: service restart; the scheduling thread is blocked and the thread is exhausted; the last scheduling continues to be blocked, and the next scheduling is missed;
- Processing strategy:
     - Expires more than 5s: Ignore this time, the current time will start to calculate the next trigger time
     - Within 5s of expiration: Trigger once immediately, and the current time will start to calculate the next trigger time


#### 5.4.7 Log callback service
When the "scheduling center" of the dispatching module is deployed as a web service, it undertakes the function of the dispatching center on the one hand, and provides API services for the executors on the other hand.

The code location of the "log callback service API service" provided by the dispatch center is as follows:
```
xxl-job-admin#com.xxl.job.admin.controller.JobApiController.callback
```

After receiving the task execution request, the "executor" executes the task, and after the execution is completed, it will call back the execution result to notify the "scheduling center":

#### 5.4.8 Task HA (Failover)
If the executors are deployed in a cluster, the dispatch center will perceive all online executors, such as "127.0.0.1:9997, 127.0.0.1:9998, 127.0.0.1:9999".

When the task "routing policy" selects "Failover (FAILOVER)", when the scheduling center initiates a scheduling request each time, it will send a heartbeat detection request to the executors in order, and the first executor detected as alive will be selected. Select and send a dispatch request.

After the scheduling is successful, you can view the "Scheduling Remarks" on the log monitoring interface, as follows;
![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_jrdI.png "Enter picture title here")

"Scheduling Remarks" can see the running track of local scheduling, the "registration method", "address list" of the executor and the "routing strategy" of the task. Under the "FAILOVER" routing strategy, the dispatch center first performs heartbeat detection on the first address, and the heartbeat fails, so it is automatically skipped, and the second heartbeat detection still fails...
Until the third address "127.0.0.1:9999" is successfully detected by the heartbeat, it is selected as the "target executor"; then a scheduling request is sent to the "target executor", and the scheduling process ends, waiting for the executor to call back the execution result.

#### 5.4.9 Scheduling log
Every time the scheduling center performs task scheduling, it will record a task log. The task log mainly includes the following three parts:

- Task information: including attributes such as "executor address", "JobHandler" and "execution parameters", which can be viewed by clicking the task ID button. According to these parameters, the specific machine and task code for task execution can be accurately located;
- Scheduling information: including "scheduling time", "scheduling result" and "scheduling log", etc., according to these parameters, you can know the specific situation when the "scheduling center" initiates a scheduling request.
- Execution information: including "execution time", "execution result" and "execution log", etc., according to these parameters, you can understand the specific situation of task execution at the "executor" end;

Scheduling log, for a single scheduling, the property description is as follows:
- Executor address: the address of the machine where the task is executed;
- JobHandler: Bean mode indicates the name of JobHandler for task execution;
- Task parameters: input parameters for task execution;
- Scheduling time: the dispatching center, the time when dispatching is initiated;
- Scheduling result: the scheduling center, the result of initiating scheduling, SUCCESS or FAIL;
- Scheduling remarks: the dispatch center, the remark information for initiating dispatch, such as the address heartbeat detection log, etc.;
- Execution time: the executor, the callback time after the task execution ends;
- Execution result: executor, task execution result, SUCCESS or FAIL;
- Execution notes: executors, notes on task execution, such as exception logs, etc.;
- Execution log: During task execution, the complete execution log printed in the business code, see "4.8 Viewing Execution Log";

#### 5.4.10 Task dependencies
Principle: Each task in XXL-JOB corresponds to a task ID. At the same time, each task supports setting the attribute "subtask ID". Therefore, the task dependency can be matched through the "task ID".

When the execution of the parent task is completed and the execution is successful, the subtask dependency will be matched according to the "subtask ID". If a subtask is matched, the execution of the subtask will be actively triggered.

In the task log interface, click the "View" button of the "Execution Notes" of the task, and you can see the log information of the matching subtask and the triggering subtask execution. If there is no information, it means that the subtask execution was not triggered. Refer to the figure below.

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_Wb2o.png "Enter picture title here")

![Enter picture description](https://www.xuxueli.com/doc/static/xxl-job/images/img_jOAU.png "Enter picture title here")

#### 5.4.11 Fully asynchronous & lightweight

- Fully asynchronous design: The business logic in the XXL-JOB system is executed on the remote executor, and the trigger process is fully asynchronously designed. Compared with directly executing business logic in the scheduling center, it greatly reduces the time occupied by scheduling threads;
     - Asynchronous scheduling: The scheduling center only sends a scheduling request once each time a task is triggered. The scheduling request is first pushed to the "asynchronous scheduling queue" and then pushed to the remote executor asynchronously
     - Asynchronous execution: The executor will store the request in the "asynchronous execution queue" and immediately respond to the dispatch center to run asynchronously.
- Lightweight design: The logic of each JOB in the XXL-JOB scheduling center is very "light". On the basis of full asynchronization, the average running time of a single JOB is basically within "10ms" (basically the network of one request overhead); therefore, it is guaranteed to use limited threads to support a large number of JOBs running concurrently;

Thanks to the above two optimizations, in theory, the scheduling center under the default configuration can support 5000 tasks concurrently and run stably;

In actual scenarios, due to the different ping delays between the scheduling center and the executor network, the different time-consuming DB reads and writes, and the different levels of task scheduling intensity, the upper limit of the task volume will fluctuate up and down.

If you need to support more tasks, you can optimize it by "increasing the number of scheduling threads", "reducing the ping delay between the scheduling center and the executor", and "improving the machine configuration".

#### 5.4.12 Balanced Scheduling
When the dispatch center is deployed in the cluster, it will automatically distribute tasks evenly, triggering components to obtain tasks related to the number of thread pools each time (the dispatch center supports custom dispatch thread pool size), avoiding the concentration of a large number of tasks on a single dispatch center cluster node;

### 5.5 Task "Run Mode" Anatomy
#### 5.5.1 "Bean pattern" task
Development steps: refer to "Chapter 3";
Principle: Each Bean pattern task is a Spring Bean class instance, which is maintained in the Spring container of the "executor" project. The task class needs to be annotated with "@JobHandler(value="name")", because the "executor" will identify the tasks in the Spring container according to the annotation. The task class needs to inherit the unified interface "IJobHandler", and the task logic is developed in the execute method, because when the "executor" receives the scheduling request from the dispatch center, it will call the execute method of "IJobHandler" to execute the task logic.

#### 5.5.2 "GLUE mode (Java)" task
Development steps: refer to "Chapter 3";
Principle: The code of each "GLUE mode (Java)" task is actually "a class code of an implementation class inherited from "IJobHandler". When the "executor" receives the scheduling request from the "scheduling center", it will pass The Groovy class loader loads this code, instantiates it into a Java object, and injects the Spring service declared in this code (please ensure that the service and class references in the Glue code exist in the "executor" project), and then calls the execute method of the object , to execute the task logic.

#### 5.5.3 GLUE mode (Shell) + GLUE mode (Python) + GLUE mode (PHP) + GLUE mode (NodeJS) + GLUE mode (Powershell)
Development steps: refer to "Chapter 3";
Principle: The source code of the script task is hosted in the dispatch center, and the script logic runs on the executor. When a script task is triggered, the executor will load the script source code to generate a script file on the executor machine, and then call the script through Java code; and write the script output log to the task log file in real time, so that the dispatch center can real-time Monitor script execution;

Currently supported script types are as follows:

     - shell script: "Shell" script task is supported when the task operation mode is selected as "GLUE mode (Shell)";
     - python script: "Python" script task is supported when the task operation mode is selected as "GLUE mode (Python)";
     - php script: "PHP" script task is supported when the task operation mode is selected as "GLUE mode (PHP)";
     - nodejs script: "NodeJS" script task is supported when the task operation mode is selected as "GLUE mode (NodeJS)";
     - powershell: "PowerShell" script task is supported when the task operation mode is selected as "GLUE mode (PowerShell)";

The script task judges the task execution result through the Exit Code, and the status code can refer to the chapter "5.15 Description of the task execution result";

#### 5.5.4 Executors
The executor is actually an embedded server with a default port of 9999 (configuration item: xxl.job.executor.port).

When the project starts, the executor will identify the "Bean mode task" in the Spring container through "@JobHandler", and manage it with the value attribute of the annotation as the key.

When the "executor" receives the scheduling request from the "scheduling center", if the task type is "Bean mode", it will match the "Bean mode task" in the Spring container, and then call its execute method to execute the task logic. If the task type is "GLUE mode", the GLue code will be loaded, the Java object will be instantiated, and the dependent Spring service will be injected (note: the Spring service injected in the Glue code must exist in the Spring container of the "executor" project) , and then call the execute method to execute the task logic.

#### 5.5.5 Task log
XXL-JOB will generate a separate log file for each scheduling request, you need to print the execution log through "XxlJobHelper.log", and the "Scheduling Center" will load the corresponding log file when viewing the execution log.

(The historical version is implemented by rewriting LOG4J's Appender, which has dependency restrictions, and this method has been abandoned in the new version)

The location where the log files are stored can be customized in the "executor" configuration file. The default directory format is: /data/applogs/xxl-job/jobhandler/"formatted date"/"primary key ID.log of database scheduling log records" .

When the child thread is enabled in the JobHandler, the child thread will print the log in the execution log of the parent thread, JobHandler, to facilitate log tracking.

### 5.6 Analysis of communication module

#### 5.6.1 A complete task scheduling communication process
     - 1. The "dispatching center" sends an http scheduling request to the "executor": the service receiving the request in the "executor" is actually an embedded server with a default port of 9999;
     - 2. "Executor" executes task logic;
     - 3. "Executor" http callback "Scheduling Center" scheduling result: The service that receives callbacks in "Scheduling Center" is a set of API services for actuators;

#### 5.6.2 Communication data encryption
When the scheduling center sends the scheduling request to the executor, two objects, RequestModel and ResponseModel, are used to encapsulate the scheduling request parameters and response data. Before communication, the bottom layer will serialize the above two objects, and perform data protocol and timestamp inspection, so To achieve the function of data encryption;

### 5.7 Task registration, automatic task discovery
Since the v1.5 version, the task cancels the "task execution machine" attribute, and instead dynamically obtains the address of the remote executor and executes it through task registration and automatic discovery.

     AppName: The unique identifier of each executor machine cluster, task registration is registered with "executor" as the smallest granularity; each task can perceive the corresponding executor machine list through its bound executor;
     Registry: See the "xxl_job_registry" table, "Executor" will periodically maintain a registration record when performing task registration, that is, the binding relationship between the machine address and AppName; "Scheduling Center" can dynamically perceive the online status of each AppName machine list;
     Executor registration: The task registration Beat period defaults to 30s; the executor registers the executor with one beat, and the dispatch center performs dynamic task discovery with one beat; the expiration time of the registration information is three beats;
     Actuator registration removal: When the executor is destroyed, it will actively report to the dispatch center and remove the corresponding executor machine information to improve the real-time performance of heartbeat registration;
    

In order to ensure that the system is "lightweight" and reduce the cost of learning and deployment, Zookeeper is not used as the registration center, and the DB method is used for task registration and discovery;

### 5.8 Task Execution Results
Since v1.6.2, the task execution result is judged by the return value "ReturnT" of "IJobHandler";
When the return value matches "ReturnT.code == ReturnT.SUCCESS_CODE", it means that the task execution is successful, otherwise it means that the task execution fails, and the error message can be called back to the dispatch center through "ReturnT.msg";
Thus, the task execution result can be conveniently controlled in the task logic;

### 5.9 Fragmented Broadcast & Dynamic Fragmentation
When the executor cluster is deployed, if the task routing strategy selects "shard broadcast", a task schedule will broadcast to trigger all executors in the corresponding cluster to execute a task, and the system will automatically pass the shard parameters; slice task;

"Shard broadcasting" performs sharding in the dimension of executors, supports dynamic expansion of executor clusters to dynamically increase the number of shards, and coordinate business processing; it can significantly improve task processing capabilities and speed when performing large-scale business operations.

"Shard Broadcast" is consistent with the normal task development process, the difference is that you can get slice parameters, and get slice parameters for slice business processing.

- Java language tasks to obtain slice parameters: BEAN, GLUE mode (Java)
```
// You can refer to the sample task "ShardingJobHandler" in the Sample sample executor to understand the trial
int shardIndex = XxlJobHelper. getShardIndex();
int shardTotal = XxlJobHelper.getShardTotal();
```
- Scripting language tasks to obtain fragmentation parameters: GLUE mode (Shell), GLUE mode (Python), GLUE mode (Nodejs)
```
// The input parameters of the script task are fixed at three, which are: task parameter, shard number, and total number of shards. Taking the Shell mode task as an example, the code to obtain fragmentation parameters is as follows
echo "Shard index = $2"
echo "Total number of shards total = $3"
```
    
Fragment parameter attribute description:

     index: current shard serial number (starting from 0), the serial number of the current executor in the executor cluster list;
     total: the total number of shards, the total number of machines in the executor cluster;

This feature applies to scenarios such as:
- 1. Fragmentation task scenario: a cluster of 10 executors processes 100,000 pieces of data, and each machine only needs to process 10,000 pieces of data, reducing the time-consuming by 10 times;
- 2. Broadcast task scenarios: broadcast executor machines run shell scripts, broadcast cluster nodes perform cache updates, etc.

### 5.10 Access Token (AccessToken)
In order to improve the security of the system, the dispatch center and the executor perform security verification, and only when the AccessTokens of both parties match are allowed to communicate;

The dispatch center and the executor can set the AccessToken through the configuration item "xxl.job.accessToken".

There are only two settings for the dispatch center and the actuator if normal communication is required;

- Setting 1: AccessToken is not set for dispatch center and executor; security verification is turned off;
- Setting 2: dispatch center and executor, set the same AccessToken;

### 5.11 Failover & Failed Retries
A complete task process includes two stages of "scheduling (scheduling center) + execution (executor)".
    
- "Failover" occurs in the scheduling phase. When the executor cluster is deployed, if an executor fails, this strategy supports automatic failover switching to a normal executor machine and completes the scheduling request process.
- "Failure retry" occurs in the two phases of "scheduling + execution". It supports customizing the number of task failure retries. When the task fails, it will actively retry according to the preset number of failed retries;

### 5.12 Actuator gray scale is online
The dispatching center is decoupled from the business, and it only needs to be deployed once and requires no maintenance for many years. However, business jobs are hosted and run in the executor, and the executor needs to be restarted when the job is online and changed, especially the Bean mode task.
Executor restarts may interrupt running tasks. However, XXL-JOB benefits from the self-built executor and self-built registration center, and can go online in grayscale to avoid the problem of task interruption caused by restarting.

Proceed as follows:
- 1. The actuator is changed to manual registration, half of the machine list is offline (Group A), and the other half of the machine list is running online (Group B);
- 2. Wait for the machine tasks in group A to finish and compile and go online; replace the registration address of the executor with group A;
- 3. Wait for group B machine tasks to finish and compile and go online; the actuator registration address is replaced with group A+group B;
operation ended;

### 5.13 Description of Task Execution Results
The system judges the task execution result according to the following criteria, which can be referred to.

-- | Bean/Glue(Java) | Glue(Shell) and other script tasks
--- | --- | ---
SUCCESS | IJobHandler.SUCCESS | 0
Failed | IJobHandler.FAIL | -1 (non-zero status code)

### 5.14 Task timeout control
Support setting the task timeout time, when the task runs overtime, it will actively interrupt the task;

It should be noted that when a task is timed out and interrupted, it is similar to the task termination mechanism (see "4.9 Terminating Running Tasks"). It also interrupts the task through "interrupt", so the business code needs to throw "InterruptedException", otherwise the function is unavailable .

### 5.15 Cross-language
XXL-JOB is a cross-language task scheduling platform, which is mainly reflected in the following aspects:
- 1. RESTful API: The dispatch center and the executor provide language-independent RESTful API services, and any third-party language can connect to the dispatch center or implement the executor. (Refer to the chapter "Scheduling Center/Actuator RESTful API")
- 2. Multi-task mode: provide more than ten task modes such as Java, Python, PHP..., please refer to the chapter "5.5 Task "running mode""; in theory, any language task mode can be expanded;
- 2. Provide an HTTP-based task handler (Bean task, JobHandler="httpJobHandler"); the business side only needs to provide relevant information such as HTTP links, without restrictions on language and platform; (refer to the chapter "Native Built-in Bean Mode Tasks" )

### 5.16 Task failure warning
Email failure alarm is provided by default, and SMS, DingTalk, etc. can be extended. If you need to add an alarm method, you only need to add an alarm implementation that implements the "com.xxl.job.admin.core.alarm.JobAlarm" interface. You can refer to "EmailJobAlarm" that provides email alarms by default.

### 5.17 Docker image construction of dispatch center
The dispatch center can be quickly built and started running with the following commands;
```
mvn clean package
docker build -t xuxueli/xxl-job-admin ./xxl-job-admin
docker run --name xxl-job-admin -p 8080:8080 -d xuxueli/xxl-job-admin
```

### 5.20 Avoid Duplicate Tasks
Scheduling intensive or time-consuming tasks may cause task blocking, and in the case of clusters, the scheduling component will be triggered repeatedly with a small probability;
In view of the above situation, it can be avoided by combining "single machine routing strategy (such as: first, consistent hash)" + "blocking strategy (such as: single machine serial, discarding subsequent scheduling)", and finally avoid task duplication.

### 5.21 Command line tasks
Natively provide a common command line task Handler (Bean task, "CommandJobHandler"); the business side only needs to provide the command line;
For example, the task parameter "pwd" will execute the command and output data;

### 5.22 Automatic log cleaning
The XXL-JOB log mainly includes the following two parts, both of which support automatic log cleaning, as follows:
- Log table data in the dispatch center: You can use the configuration item "xxl.job.logretentiondays" to set the number of days for log table data to be saved, and expired logs will be automatically cleared; for details, please refer to the above configuration instructions;
- Executor log file data: You can use the configuration item "xxl.job.executor.logretentiondays" to set the number of days to save log file data, and expired logs will be automatically cleared; for details, please refer to the above configuration instructions;

### 5.23 Scheduling result loss processing
The executor will lose the task scheduling result due to network jitter callback failure or abnormal conditions such as downtime. Since the scheduling center relies on the executor callback to perceive the scheduling results, it will cause the scheduling log to always be in the "running" state.

To solve this problem, the scheduling center provides built-in components to handle it. The logic is: if the scheduling record stays in the "running" state for more than 10 minutes, and the corresponding executor heartbeat registration fails and is offline, the local scheduling will be actively marked as failed;


## 6. Scheduling Center/Actuator RESTful API
XXL-JOB is a cross-platform, cross-language task scheduling specification and protocol.

For Java applications, you can directly access and use the dispatch center through the official dispatch center and executor. You can refer to the "Quick Start" section above.

For non-Java applications, multi-language support can be easily realized with the help of XXL-JOB's standard RESTful API.

- Dispatch center RESTful API:
     - Description: The API provided by the dispatch center for the executor; it is not limited to the use of the official executor, and third parties can use this API to implement the executor;
     - API list: executor registration, task result callback, etc.;
- Actuator RESTful API:
     - Description: The API provided by the executor to the dispatch center; the official executor has been implemented by default, and the third-party executor needs to be implemented and provided to the dispatch center;
     - API list: task trigger, task termination, task log query...etc;

The RESTful API here is mainly used for non-Java language custom personalized executors to achieve cross-language. In addition, if you need to operate the dispatch center through the API, you can personalize and expand the "dispatch center RESTful API" and use it.

### 6.1 Dispatching Center RESTful API

API service location: com.xxl.job.core.biz.AdminBiz ( com.xxl.job.admin.controller.JobApiController )
API service request reference code: com.xxl.job.adminbiz.AdminBizTest

#### a. Task callback
```
Description: After the executor finishes executing the task, it is used when calling back the task result

------

Address format: {dispatch center root address}/api/callback

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     [{
         "logId":1, // ID of this schedule log
         "logDateTim":0, // The log time of this scheduling
         "handleCode":200, // 200 means the task is executed normally, 500 means it failed
         "handleMsg": null
         }
     }]

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```
    
#### b. Actuator registration
```
Description: Used when the executor is registered, the scheduling center will perceive the registered executor in real time and initiate task scheduling

------

Address format: {dispatch center root address}/api/registry

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     {
         "registryGroup": "EXECUTOR", // fixed value
         "registryKey": "xxl-job-executor-example", // executor AppName
         "registryValue":"http://127.0.0.1:9999/" // Actuator address, built-in service and address
     }

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```

#### c. Removal of executor registration
```
Note: It is used when the executor is registered and removed, and the executor after the registration is removed does not participate in task scheduling and execution

------

Address format: {dispatch center root address}/api/registryRemove

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     {
         "registryGroup": "EXECUTOR", // fixed value
         "registryKey": "xxl-job-executor-example", // executor AppName
         "registryValue":"http://127.0.0.1:9999/" // Actuator address, built-in service and address
     }

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```

### 6.2 Actuator RESTful API

API service location: com.xxl.job.core.biz.ExecutorBiz
API service request reference code: com.xxl.job.executorbiz.ExecutorBizTest

#### a. Heartbeat detection
```
Description: Used when the dispatch center detects whether the executor is online

------

Address format: {actuator embedded service root address}/beat

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```

#### b. Busy detection
```
Description: Used when the dispatch center detects whether the specified task on the specified executor is busy (running)

------

Address format: {actuator embedded service root address}/idleBeat

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     {
         "jobId":1 // job ID
     }

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```

#### c. Trigger tasks
```
Description: Trigger task execution

------

Address format: {executor embedded service root address}/run

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     {
         "jobId":1, // job ID
         "executorHandler": "demoJobHandler", // task ID
         "executorParams": "demoJobHandler", // task parameters
         "executorBlockStrategy":"COVER_EARLY", // Task blocking strategy, optional values refer to com.xxl.job.core.enums.ExecutorBlockStrategyEnum
         "executorTimeout":0, // Task timeout, in seconds, takes effect when it is greater than zero
         "logId":1, // ID of this schedule log
         "logDateTime":1586629003729, // The log time of this scheduling
         "glueType":"BEAN", // task mode, refer to com.xxl.job.core.glue.GlueTypeEnum for optional values
         "glueSource": "xxx", // GLUE script code
         "glueUpdatetime":1586629003727, // GLUE script update time, used to determine whether the script has changed and whether it needs to be refreshed
         "broadcastIndex":0, // fragmentation parameter: current fragmentation
         "broadcastTotal":0 // fragmentation parameter: total fragmentation
     }

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```

#### f. Terminate task
```
Description: terminate the task

------

Address format: {executor embedded service root address}/kill

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     {
         "jobId":1 // job ID
     }
    

Response data format:
     {
       "code": 200, // 200 means normal, other failures
       "msg": null // error message
     }
```

#### d. View the execution log
```
Description: Terminate the task and load in scrolling mode

------

Address format: {actuator embedded service root address}/log

Header:
     XXL-JOB-ACCESS-TOKEN : {request token}
 
The request data format is as follows, placed in RequestBody, JSON format:
     {
         "logDateTim":0, // The log time of this scheduling
         "logId":0, // ID of this schedule log
         "fromLineNum":0 // log start line number, scroll to load log
     }

Response data format:
     {
         "code":200, // 200 means normal, other failures
         "msg": null // error message
         "content":{
             "fromLineNum":0, // This request, log start line number
             "toLineNum":100, // This request, the log end line number
             "logContent": "xxx", // log content of this request
             "isEnd":true // Whether all logs are loaded
         }
     }
```



## 7. version update log
### 7.1 version V1.1.x, new features[2015-12-05]
**【In V1.1.x version, XXL-JOB is officially applied to our company, and the internal customized alias is "Ferrari". The latest version is recommended for new access applications】**
- 1. Simple: Support CRUD operations on tasks through web pages, easy to operate, and get started in one minute;
- 2. Dynamic: Support dynamic modification of task status, dynamic pause/resume task, and take effect immediately;
- 3. Service HA: Task information is persisted in mysql, and Job service naturally supports clusters to ensure service HA;
- 4. Task HA: When a Job service is down, the task will be smoothly assigned to another surviving service. Even if all the services are down, when restarting or compensating for the execution of lost tasks;
- 5. A task will only be executed on one of the servers;
- 6. Serial execution of tasks;
- 7. Support custom parameters;
- 8. Support remote task execution termination;

### 7.2 version V1.2.x, new features[2016-01-17]
- 1. Support task grouping;
- 2. Support "local tasks" and "remote tasks";
- 3. The underlying communication supports two methods, Servlet method + JETTY method;
- 4. Support "task log";
- 5. Support "serial execution" and parallel execution;

Note: The V1.2 version splits the system architecture into functions according to:

- Scheduling module (scheduling center): responsible for managing scheduling information and sending scheduling requests according to scheduling configuration;
- Execution module (executor): responsible for receiving scheduling requests and executing task logic;
- Communication module: responsible for information communication between the scheduling module and the task module;
	advantage:

- Decoupling: the task module provides a task interface, the scheduling module maintains scheduling information, and the business is independent of each other;
- High scalability;
- stability;

### 7.3 version V1.3.0, new features[2016-05-19]
- 1. Abandon the "local task" mode, recommend the use of "remote task", which is easy to decouple the system, and the JobHandler corresponding to the task is collectively referred to as "executor";
- 2. Abandon the "servlet" method for underlying system communication. It is recommended to use the JETTY method, scheduling + callback two-way communication, and reconstruct the communication logic;
- 3. UI interaction optimization: the expansion state of the left menu is optimized, the selected state of the menu item is optimized, and the opening form of the task list has compression optimization;
- 4. [Important] "Actuator" is subdivided into two development modes: BEAN and GLUE. See the introduction below:

An introduction to the Actuator pattern:
- BEAN mode executor: each executor is a Bean instance of Spring, and XXL-JOB identifies and schedules the executor through the annotation @JobHandler;
-GLUE mode executor: each executor corresponds to a piece of code, online web editing and maintenance, dynamic compilation takes effect, and the executor is responsible for loading and executing GLUE code;

### 7.4 version V1.3.1, new features[2016-05-23]
- 1. Update the project directory structure:
- /xxl-job-admin -------------------- [Scheduling Center]: Responsible for managing scheduling information and sending scheduling requests according to scheduling configuration;
- /xxl-job-core ----------------------- public dependencies
- /xxl-job-executor-example ------ [executor]: responsible for receiving scheduling requests and executing task logic;
- /db ---------------------------------- Table creation script
- /doc --------------------------------- User Manual
- 2. Based on the new directory structure, the user manual has been upgraded;
- 3. Optimized some interactions and UI;

### 7.5 version V1.3.2, new features[2016-05-28]
- 1. Scheduling logic for transaction wrapping;
- 2. The executor asynchronously calls back the execution log;
- 3. [Important] On the basis of the HA support of the "Scheduling Center", the Failover support of the executor is extended to support the configuration of multiple execution period addresses;

### 7.6 version V1.4.0 new features[2016-07-24]
- 1. Task dependency: It is realized by event triggering. When the task is successfully executed and called back, it will actively trigger the scheduling of subtasks. Multiple subtasks are separated by commas;
- 2. The underlying implementation code of the executor is heavily refactored, and the underlying table creation script is optimized;
- 3. Optimization of task thread grouping logic in the executor: Previously, thread grouping was performed according to the executor JobHandler. When multiple tasks reuse JobHandler, it will cause mutual blocking. Now it is changed to group task threads according to dispatch center tasks, and tasks and task execution are isolated from each other;
- 4. Optimizing the actuator scheduling communication scheme, implementing the proposed RPC communication protocol through Hex + HC, optimizing the maintenance and analysis process of communication parameters;
- 5. Scheduling center, new/edit task, interface property adjustment:
     - 5.1. Remove the "JobName" attribute from the task adding/editing interface, and change the attribute to be automatically generated by the system: This field was mainly used to uniquely mark a task in the "Scheduling Center" before, and it has little practical significance, so the plan has been diluted Delete this field and change it to a UUID generated by the system, thus simplifying the operation of creating new tasks;
     - 5.2. Removed the "GLUE mode" check box position adjustment in the task adding/editing interface, and changed it to be close to the right side of the "JobHandler" input box;
     - 5.3. The "Alarm Threshold" attribute was removed from the task adding/editing interface;
     - 5.4. The "Subtask Key" attribute is removed from the task adding/editing interface. The global task Key of each task can be obtained from the task list. When the task is completed and successfully executed, the subtask will be matched according to the subtask key and actively Trigger a subtask execution;
- 6. Bug fixes:
     - 6.1. The actuator jetty is closed and optimized to solve a problem that may cause jetty to fail to close;
     - 6.2. When the executor task is terminated, the execution queue callback is optimized to solve a problem that the task cannot be called back;
     - 6.3. Optimized the list pagination parameters in the scheduling center to solve a problem caused by the server limiting the length of the post;
     - 6.4. The executor Jobhandler annotation is optimized to solve a problem that the container cannot load the JobHandler due to transaction proxy;
     - 6.5, remote scheduling optimization, disable the retry strategy, and solve a problem that may cause repeated calls;

Tips: The historical version (V1.3.x) has been Released to a stable version and is entering the maintenance phase. For the address, see the branch [V1.3](https://github.com/xuxueli/xxl-job/tree/v1.3 ). New features will be continuously updated on the master branch.

### 7.7 version V1.4.1 new features[2016-09-06]
- 1. The project is successfully pushed to the maven central warehouse, and the central warehouse address and dependencies are as follows:
     ```
     <!-- http://repo1.maven.org/maven2/com/xuxueli/xxl-job-core/ -->
     <dependency>
         <groupId>com.xuxueli</groupId>
         <artifactId>xxl-job-core</artifactId>
         <version>${latest stable version}</version>
     </dependency>
     ```
- 2. In order to adapt to the rules of the central warehouse, the project groupId is changed from com.xxl to com.xuxueli.
- 3. The system version is not maintained in the project and pom, and each sub-module is configured separately to solve the problem that the sub-modules cannot be compiled separately;
- 4. Underlying RPC communication, the byte length statistical rules of the transmitted data are optimized, which can save 50% of the data transmission volume;
- 5. IJobHandler cancels the return value of the task. The original judgment of the execution status is based on the return value. The logic is changed to: the default task execution is successful, and the task execution fails only when an exception is caught.
- 6. System public bullet box function, plug-in;
- 7. The underlying table structure, indicating uniform capitalization;
- 8. Modify the ContentType of the JSON response of the dispatch center and the exception handler, and fix the problem that the browser does not recognize it;

### 7.8 version V1.4.2 new features[2016-09-29]
- 1. Push the new version V1.4.2 to the central warehouse, and the major version V1.4 enters the maintenance stage;
- 2. When the task is added, the task list offset problem is fixed;
- 3. Fix a style disorder problem caused by bootstrap not supporting the overlapping of modal boxes, which will occur when editing tasks;
- 4. When the scheduling timeout and the Handler cannot be matched, the scheduling status is optimized;
- 5. The problem that the task cannot be terminated due to the catch exception is given, and the solution is given, see the document;

### 7.9 Version V1.5.0 Features[2016-11-13]
- 1. Task registration: The executor will automatically register tasks periodically, and the dispatch center will automatically discover the registered tasks and trigger execution.
- 2. Added parameter "AppName" in "Executor": it is the unique identifier AppName of each actuator cluster, and the AppName is used as the object for automatic registration periodically.
- 3. A new column "Executor Management" in the dispatch center: manage online executors, and automatically discover registered executors through the attribute AppName. Only managed executors are allowed to be used;
- 4. Change the "task group" attribute to "executor": each task needs to be bound to a specified executor, and the scheduling address is obtained through the bound executor;
- 5. Abandon the "task machine" attribute: automatically discover the registered remote executor address and trigger a scheduling request through the executor bound to the task.
- 6. Added DBGlueLoader in "Public Dependencies", which implements the loader of GLUE source code based on native jdbc, reducing third-party dependencies (mybatis, spring-orm, etc.); streamlines and optimizes the configuration of executors (for GLUE tasks), reducing the need for getting started difficulty;
- 7. Table structure adjustment, underlying reconstruction optimization;
- 8. Automatic registration and discovery of the "dispatch center", failover: The dispatch center automatically registers periodically, and when the task is called back, it can perceive the addresses of all online dispatch centers, and the task is called back through failover to avoid the risk of a single point of callback.

### 7.10 Version V1.5.1 Features[2016-11-13]
- 1. Underlying code refactoring and logic optimization, POM cleaning and CleanCode;
- 2. Servlet/JSP Spec is set to 3.0/2.2
- 3. Spring is upgraded to version 3.2.17.RELEASE;
- 4. Jetty upgrade version to 8.2.0.v20160908;
- 5. V1.5.0 and V1.5.1 have been pushed to the Maven central warehouse;

### 7.11 Version V1.5.2 Features[2017-02-28]
- 1. IP tool class obtains IP logic optimization, IP static cache;
- 2. Both the actuator and the dispatch center support custom registration IP addresses; solve the problem of wrong network card registration when the machine has multiple network cards;
- 3. Fix the problem of generating multiple log files when the task is executed across days;
- 4. The underlying log is adjusted, and the non-sensitive log level is adjusted to debug;
- 5. Upgrade the c3p0 version of the database connection pool;
- 6. Optimizing the log4j configuration of the executor, removing invalid attributes;
- 7. Underlying code refactoring and logic optimization and CleanCode;
- 8. GLUE dependency injection logic optimization, support alias injection;

### 7.12 Version V1.6.0 Features[2017-03-13]
- 1. The communication scheme is upgraded, the original HEX-based communication model is adjusted to the HTTP-based B-RPC communication model;
- 2. The executor supports manual setting of the execution address list, and provides a switch to switch between using a registered address or a manually set address;
- 3. Executor routing rules: first, last, polling, random, consistent HASH, least frequently used, least recently used, failover;
- 4. Standardize the unified thread model and unified thread destruction scheme (through the listener or stop method, the thread is destroyed when the container is destroyed; the Daemon method is sometimes not ideal);
- 5. Standardize system configuration data and manage them uniformly through configuration files;
- 6. CleanCode, to clean up invalid historical parameters;
- 7. The underlying extended data structure and related table structure adjustments;
- 8. The new task defaults to non-running state;
- 9. The update logic of task instances in GLUE mode is optimized, the original update is based on the timeout time, and the update is based on the version number, and the version number of the source code changes is increased by one;

### 7.13 Version V1.6.1 Features[2017-03-25]
- 1. Rolling log;
- 2. Interactive reconstruction of WebIDE;
- 3. Enhanced communication verification, effectively filtering abnormal requests;
- 4. Permission enhancement verification, using dynamic login TOKEN (internal SSO is recommended);
- 5. The database configuration is optimized to solve the problem of garbled characters;

### 7.14 Version V1.6.2 Features[2017-04-25]
- 1. Operation report: supports real-time viewing of operation data, such as the number of tasks, scheduling times, number of executors, etc.; and scheduling reports, such as scheduling date distribution diagram, scheduling success distribution diagram, etc.;
- 2. JobHandler supports setting the task return value, which can conveniently control the task execution result in the task logic;
- 3. When the resource path contains spaces or Chinese, when the resource file cannot be loaded, the exception information cannot be accurately viewed.
- 4. Routing policy optimization: loop and LFU routing policy counter self-increment without upper limit problem and the problem that the first routing pressure is concentrated on the first machine is fixed;

### 7.15 Version V1.7.0 Features[2017-05-02]
- 1. Script tasks: support the development and operation of script tasks in GLUE mode, including Shell, Python and Groovy scripts;
- 2. Add spring-boot type actuator example project;
- 3. Upgrade jetty version to 9.2;
- 4. The task running log removes the log4j component dependency, and changes it to the underlying independent implementation, thus canceling the dependency restriction on the log component;
- 5. The executor removes the GlueLoader dependency and implements it in push mode, so that GLUE source code loading no longer depends on JDBC;
- 6. Obtain the project name when logging in to intercept Redirect, and solve the problem of jumping to 404 when it is not published according to the directory;

### 7.16 Version V1.7.1 Features[2017-05-08]
- 1. The reading and writing code of the operation log is unified as UTF-8, which solves the problem of garbled logs in the windows environment;
- 2. The communication timeout time is limited to 10s to avoid scheduling thread occupation under abnormal circumstances;
- 3. Actuator, server startup, destruction and registration logic adjustment;
- 4. JettyServer shutdown logic optimization, repair the problem that the executor cannot be shut down normally, which leads to port occupation and frequent printing of c3p0 logs;
- 5. When sub-threads are enabled in JobHandler, sub-threads are supported to output execution logs and view them through Rolling.
- 6. Task log cleaning function;
- 7. The bullet frame components are uniformly replaced with layer;
- 8. Upgrade quartz version to 2.3.0;

### 7.17 Version V1.7.2 Features[2017-05-17]
- 1. Blocking processing strategy: the processing strategy when the scheduling is too intensive and the executor is too late to process. The strategies include: stand-alone serial (default), discarding subsequent scheduling, and overriding previous scheduling;
- 2. Failure handling strategy; handling strategy when scheduling fails, strategies include: failure alarm (default), failure retry;
- 3. The communication timestamp timeout time is adjusted to 180s;
- 4. The executor is completely decoupled from the database, but the executor needs to configure the dispatch center cluster address. The dispatch center provides API for actuator callback and heartbeat registration services, cancels the internal jetty of the dispatch center, adjusts the heartbeat cycle to 30s, and heartbeat failure to triple heartbeat;
- 5. Fixed the missing problem when executing parameter editing;
- 6. New task test demo is added to facilitate task logic testing during development;

### 7.18 Version V1.8.0 Features[2017-07-17]
- 1. Optimize the task Cron update logic, change it to rescheduleJob, and prevent repeated cron settings;
- 2. The API callback service failure status code is optimized to facilitate troubleshooting;
- 3. XxlJobLogger's log multi-parameter support;
- 4. The "busy transfer" mode is added to the routing policy: the idle detection is performed in sequence, and the first machine that succeeds in the idle detection is selected as the target executor and initiates scheduling;
- 5. Routing strategy code refactoring;
- 6. Fixed the duplicate registration problem of actuators;
- 7. Task threads are automatically destroyed after 30 byes, reducing the consumption of invalid threads for low-frequency tasks.
- 8. Batch callback of executor task execution results, reduce callback frequency and improve executor performance;
- 9. For the springboot version of the actuator, the XML configuration is canceled and changed to the class configuration method;
- 10. Execution log, which supports filtering logs according to the running "status";
- 11. Optimization of task registration detection logic in dispatch center;

### 7.19 Version V1.8.1 Features[2017-07-30]
- 1. Fragment broadcast task: When the executor cluster is deployed, if the task routing policy selects "fragment broadcast", a task scheduling will broadcast and trigger all executors in the cluster to execute a task, and the fragment can be processed according to the fragmentation parameters Task;
- 2. Dynamic sharding: shard broadcast tasks are sharded in the dimension of executors, and support dynamic expansion of executor clusters to dynamically increase the number of shards and coordinate business processing; tasks can be significantly improved when performing large-scale business operations processing power and speed.
- 3. The executor JobHandler prohibits naming conflicts;
- 4. The address list of the executor cluster is naturally sorted;
- 5. Scheduling center, DAO layer code streamlining and optimization and new test case coverage;
- 6. The API service of the dispatching center is changed to a self-developed RPC form, and the underlying communication model is unified;
- 7. Added dispatch center API service test demo, which facilitates API expansion and testing in the dispatch center;
- 8. The task list page is interactively optimized, the task list is automatically refreshed when the executor group is replaced, and the current executor is positioned by default when creating a new task;
- 9. Access token (accessToken): In order to improve system security, the dispatch center and the actuator perform security verification, and only when the AccessTokens of both parties match are allowed to communicate;
- 10. Springboot version actuator, upgraded to version 1.5.6.RELEASE;
- 11. Unified maven dependency version management;

### 7.20 Version V1.8.2 Features[2017-09-04]
- 1. Construction of project homepage: provide Chinese and English documents: https://www.xuxueli.com/xxl-job
- 2. JFinal Executor Sample sample project;
- 3. Event triggering: In addition to "Cron mode" and "task-dependent mode" to trigger task execution, it supports event-based trigger task mode. The scheduling center provides an API service that triggers a single execution of a task, which can be flexibly triggered according to business events.
- 4. Actuator removal: When the actuator is destroyed, the dispatch center is actively notified and the corresponding actuator node is removed to improve the timeliness of actuator status perception.
- 5. When the executor manually sets the IP, it will be bound to the Host;
- 6. Standardize the project directory to facilitate the expansion of multiple actuators;
- 7. Solve the problem when the actuator callback URL does not support HTTPS configuration;
- 8. Before the executor callback thread is destroyed, the data in the queue is called back in batches to prevent the loss of task results;
- 9. When the task monitoring thread of the dispatching center is destroyed, batch alarms will be sent to the failed tasks to prevent the loss of alarm information;
- 10. Solve the SimpleDateFormat concurrency problem when the task log file path timestamp is formatted;

### 7.21 Version V1.9.0 Features[2017-12-29]
- 1. Add Nutz actuator Sample project;
- 2. The new task operation mode "GLUE mode (NodeJS)" supports NodeJS script tasks;
- 3. Script tasks such as Shell, Python and Nodejs support obtaining fragmentation parameters;
- 4. Failed retry, complete support: when the dispatching center fails to schedule and the "failed retry" strategy is enabled, it will automatically retry once; the execution of the executor fails and the failed retry status is called back (the return value of the failed retry status is added ), it will also automatically retry once;
- 5. Failure alarm policy extension: By default, email failure alarms are provided, and text messages can be extended, etc., and the location of the extension code is "JobFailMonitorHelper.failAlarm";
- 6. The actuator port supports automatic generation (when it is less than or equal to 0), to avoid port definition conflicts;
- 7. Scheduling report optimization, support time interval screening;
- 8. The Log component supports the output of exception stack information, and the bottom layer is optimized;
- 9. The alarm email style is optimized, adjusted to a table format, and the email component is adjusted to commons-email to simplify email operations;
- 10. Project dependencies are fully upgraded to newer stable versions, such as spring, jackson, etc.;
- 11. Task log, which records the information of the machine that initiated the scheduling;
- 12. Interactive optimization, such as login and logout;
- 13. The task Cron length is extended to 128 bits, and the responsible type Cron setting is supported;
- 14. Interactive optimization of executor address entry, the address length is extended to 512 bits, and large-scale executor cluster configuration is supported;
- 15. The task parameter "IJobHandler.execute" is changed to "String params" to enhance the versatility of input parameters.
- 16. IJobHandler provides the init/destroy method, which supports additional operations when the corresponding task thread is initialized and destroyed;
- 17. The task annotation is adjusted to "@JobHandler", which is unified with the task abstract interface;
- 18. Fix the problem that the task monitoring thread is blocked by time-consuming tasks;
- 19. Fix the problem that the task monitoring thread cannot monitor the task trigger and execution status are not 0;
- 20. The executor dynamic proxy object intercepts the execution of non-business methods;
- 21. Fix the problem that JobThread captures Error and does not update JobLog;
- 22. Fix the problem of disordered styles when the menus on the left side of the task list interface are merged;
- 23. The dispatch center project log configuration is changed to xml file format;
- 24. The Log address format is compatible and supports non-"/" ending path configuration;
- 25. Adjust the log level of the underlying system to clean up the legacy code;
- 26. SQL optimization for table creation, support for synchronous creation of libraries and tables with specified codes;
- 27. System security optimization, MD5 encryption is performed when logging in Token to write Cookie, and HttpOnly is enabled for Cookie at the same time;
- 28. The "Task ID" attribute is added, and the "JobKey" attribute is removed. The former assumes all functions, which is convenient for subsequent enhancement of task-dependent functions.
- 29. The problem of task cycle dependency is fixed, avoiding the infinite cycle of scheduling caused by the duplication of subtasks and parent tasks;
- 30. A new filter condition "task description" is added to the task list to quickly retrieve tasks;
- 31. Periodic cleaning function of the executor Log file: a new configuration item ("xxl.job.executor.logretentiondays") for the executor will save the log, and the log file will be automatically deleted when it expires.

### 7.22 Version V1.9.1 Features[2018-02-22]
- 1. Internationalization: The dispatch center realizes internationalization, supports Chinese and English, and the default is Chinese.
- 2. Added a status item "Running" to the scheduling report;
- 3. Scheduling report optimization, report SQL optimization and new LocalCache cache (caching time 60s), improve report loading speed under large amount of data;
- 4. Fix the garbled problem of resource files when packaging and deploying;
- 5. Fix the problem that scrolling to the top of the new version of chrome fails;
- 6. Optimized loading of dispatch center configuration, canceled strong dependence on configuration file name, and supported loading disk configuration;
- 7. Fix the problem that the script task Log file is not closed normally;
- 8. Project dependencies are fully upgraded to newer stable versions, such as spring, jackson, etc.;

### 7.23 Version V1.9.2 Features[2018-10-05]
- 1. Task timeout control: Add task attribute "task timeout time", and support customization, the task will actively interrupt the task when it runs overtime;
- 2. Number of task failure retries: Add task attribute "Failure retries" and support customization. When a task fails, it will actively retry according to the preset number of failed retries; at the same time, it will converge and discard other failed retries Test strategies, such as scheduling failure, execution failure, status code failure, etc.;
- 3. The new task operation mode "GLUE mode (PHP)" supports php script tasks;
- 4. New task operation mode "GLUE mode (PowerShell)", supports PowerShell script tasks;
- 5. Scheduling is fully asynchronous processing: after the task is triggered, it is pushed to the scheduling queue, and multi-threaded concurrently processes the scheduling request, which improves the task scheduling rate and avoids the problem of quartz scheduling thread blocking caused by network problems;
- 6. Optimization of executor task results placement: when the executor callback fails, the task result is written to the disk, and the callback task result is retried when the executor is restarted or the network is restored, so as to prevent the loss of task execution results;
- 7. The task log query speed has been greatly improved: the search speed of millions of data volumes has been increased by 1000 times;
- 8. The scheduling center provides API services, and supports operations such as querying, adding, updating, starting and stopping tasks through API services;
- 9. Changed the parameter placeholder of the underlying self-developed Log component to "{}", and fixed the problem that the parameter mismatch caused an error when printing the log with parameters;
- 10. The task callback result is optimized, and it is supported to be displayed in the Rolling log, which is convenient for troubleshooting;
- 11. Compatibility optimization of underlying LocalCache components, support compilation and deployment of jdk9, jdk10 and above;
- 12. The alarm email is fixed in UTF-8 encoding format, and the email garbled problem caused by machine encoding is fixed;
- 13. The failure alarm information is displayed in the alarm email;
- 14. The alarm mailbox supports SSL configuration;
- 15. Fixed File.separator incompatibility issue under Windows machine;
- 16. Optimized the script task exception Log output;
- 17. Task thread stop variable modifier optimization;
- 18. Script task Log file stream closing optimization;
- 19. Fixed task report success, failure and in-progress statistics;
- 20. The core relies on Core internal internationalization processing;
- 21. The default number of Quartz threads is adjusted to 50;
- 22. Added "Run Report" on the left menu;
- 23. When the executor manually sets the IP, cancel the operation of binding the host. This IP is only used for the registration of the executor; fix the problem that the host of the executor cannot be bound when specifying the external network IP;
- 24. Cancel the restriction that parent-child tasks cannot be repeated, and support special scenarios such as cyclic task triggering;
- 25. The task trigger type is marked in the task scheduling notes, such as Cron trigger, parent task trigger, API trigger, etc., to facilitate troubleshooting of scheduling logs;
- 26. Fix the thread safety problem of the underlying log component SimpleDateFormat;
- 27. The communication thread of the executor is optimized, and the corePoolSize is reduced from 256 to 32;
- 28. The status field type optimization of the task log table;
- 29. GLUE script file automatic cleaning function, timely clean up expired script files;
- 30. Optimize the switching of the actuator registration method, actively synchronize the online machine when switching automatic registration, and avoid the problem that the actuator is empty;
- 31. Cross-platform: In addition to providing more than a dozen task modes such as Java, Python, PHP, etc., a new HTTP-based task mode is provided;
- 32. The underlying RPC serialization protocol is adjusted to hessian2;
- 33. Fix the problem that the table field "t.order" conflicts with the database keyword and the query fails.
- 34. Task attribute enumeration "task mode, blocking strategy" internationalization optimization;
- 35. Shard task failure retry optimization, only retry the currently failed shard;
- 36. Dynamic parameter transfer is supported when a task is triggered, and both the scheduling center and the API service provide dynamic parameter functions;
- 37. Adjust the field type of task execution log and scheduling log, change it to text type and cancel the word limit;
- 38. Adjust the field type of GLUE task script, change it to mediumtext type, and increase the upper limit of GLUE length;
- 39. The log output of the task monitoring thread is optimized, and the monitoring log of the running task is changed to the debug level to reduce the amount of non-core logs;
- 40. Project dependencies are fully upgraded to newer stable versions, such as spring, Jackson, groovy, etc.;
- 41. docker support: the dispatch center provides Dockerfile to facilitate and quickly build docker images;

### 7.24 Version V2.0.0 Release Notes[2018-11-04]
- 1. The scheduling center is migrated to springboot;
- 2. The underlying communication components are migrated to xxl-rpc;
- 3. Containerization: provide the official docker image, and update and push dockerhub (docker pull xuxueli/xxl-job-admin) in real time to further realize the out-of-the-box use of the product;
- 4. Added the frameless executor sample project "xxl-job-executor-sample-frameless". Does not rely on third-party frameworks, only needs the main method to start and run the executor;
- 5. Command line task: natively provide a general command line task Handler (Bean task, "CommandJobHandler"); the business side only needs to provide the command line;
- 6. Task status optimization, only running status "NORMAL" tasks are associated with quartz, reducing the pressure on quartz underlying data storage and scheduling;
- 7. Task status specification: The new task defaults to the stop state, and the task status remains unchanged when the task is updated;
- 8. The logic of IP acquisition is optimized, traversing the network card first to obtain the available IP;
- 9. The new API service interface of the task returns the task ID, which is convenient for the caller;
- 10. Component optimization, removing the dependence on spring: non-spring applications use "XxlJobExecutor", and spring applications use "XxlJobSpringExecutor" as the actuator component;
- 11. The task RollingLog display logic is optimized, and the problem that the overtime task cannot be viewed is fixed;
- 12. A number of UI components have been upgraded to the latest version, such as: CodeMirror, Echarts, Jquery, etc.;
- 13. The project depends on upgrading groovy to a newer stable version; pom cleaning;
- 14. Subtask failure retry retry logic optimization, when a subtask fails, it will actively retry according to its preset failed retry times

### 7.25 Version v2.0.1 Release Notes[2018-11-09]
- 1. Fix the folding animation problem of the left menu;
- 2. The default value of the schedule report date distribution chart is unified;
- 3. Freemarker fixes the problem of adding thousandths to numbers by default, and solves the problem that the log ID is separated and causes the log to fail to be viewed;
- 4. The underlying communication components are upgraded, and the problem of invalid waiting when the communication is abnormal is fixed;
- 5. Fix the problem that jetty stops after the actuator starts;

### 7.26 Version v2.0.2 Release Notes[2019-04-20]
- 1. Optimization of the underlying communication scheme: upgrade the newer version xxl-rpc, adjust from the "JETTY" scheme to the "NETTY_HTTP" scheme, the executor is embedded with netty-http-server to provide services, and the dispatch center reuses container ports to provide services;
- 2. The task alarm logic adjustment is changed to be triggered by scanning failure logs. On the one hand, it accurately scans failed tasks to reduce the scanning range; on the other hand, cancels the memory queue to reduce thread memory consumption;
- 3. Quartz triggers the thread pool to be discarded and replaced with "XxlJobThreadPool", reducing the consumption caused by thread switching and memory usage, and improving scheduling performance;
- 4. The scheduling thread pool is isolated and split into two thread pools, "Fast" and "Slow". During the 1-minute window period, the task takes 500ms and exceeds 10 times. During this window period, it is judged as a slow task, and the slow task is automatically downgraded Enter the "Slow" thread pool to avoid running out of scheduling threads and improve system stability;
- 5. The JobHandler is reinitialized when the executor is hot deployed, and the "jobhandler naming conflicts." problem caused by this is fixed;
- 6. Added the loading cache of Class to solve the problem of OOM caused by insufficient space in the method area of jvm due to frequent loading of Class;
- 7. Tasks support the replacement of bound executors to facilitate group transfer and management of tasks;
- 8. The dispatching center alarm mail sending component is changed to "spring-boot-starter-mail";
- 9. The remember password function is optimized, it will be remembered permanently when selected; if it is not selected, close the browser and log out;
- 10. Project dependencies are upgraded to newer stable versions, such as quartz, spring, jackson, groovy, xxl-rpc, etc.;
- 11. Streamline projects and cancel third-party dependencies, such as commons-collections4, commons-lang3;
- 12. The executor callback log placement scheme reuses the RPC serialization scheme and removes the Jackson dependency;
- 13. Underlying Log tuning, the application terminates normally and cancels the printing of exception stack information;
- 14. Interactive optimization, try to avoid opening new page windows; only WebIDE supports new page opening, and provides a quick window close button; task start, stop, delete, trigger and other light operation prompts are changed to toast mode,
- 15. Task suspension and deletion optimization to avoid dirty data caused by incomplete quartz delete;
- 16. Task callback, heartbeat registration success log optimization, non-core regular log adjustment to debug level, reducing redundant log output;
- 17. Adjust the default interval of the home page report to this week to avoid too much log volume and slow query;
- 18. Fixed the problem that the LRU routing update was not timely;
- 19. Optimized the sending logic of task failure warning emails;
- 20. The scheduling log sorting logic is adjusted to be in reverse order according to the scheduling time, compatible with primary key discontinuous log storage components such as TIDB;
- 21. Optimizing the graceful shutdown of the actuator;
- 22. Connection pool configuration optimization, enhanced connection validity verification;
- 23. JobHandler#msg length limit, repair the problem of memory overflow caused by excessively long logs under abnormal circumstances;
- 24. Upgrade xxl-rpc to a newer version, and fix the compatibility problem of springboot 2.x version;

### 7.27 Version v2.1.0 Release Notes[2019-07-07]
- 1. Self-developed scheduling components, removing quartz dependencies: on the one hand, it is to simplify the system and reduce redundant dependencies, and on the other hand, it is to provide controllability and stability of the system;
     - Trigger: a single node triggers periodically, running events such as delayqueue;
     - Scheduling: cluster competition, load mode collaborative processing, lock competition-update trigger information-push time wheel-lock release-lock competition;
- 2. Restructuring of the underlying table structure: remove 11 quartz-related tables, and optimize and sort out the existing table structure;
- 3. The primary key of the task log is adjusted to the long data type to prevent data overflow in the case of massive logs;
- 4. Reconstruction of the underlying thread model: remove the Quartz thread pool to reduce system thread and memory overhead;
- 5. User management: support online management system users, there are two roles of administrator and ordinary user;
- 6. Permissions management: Permissions are controlled in the executor dimension, administrators have full permissions, and ordinary users need to be assigned executor permissions before allowing related operations;
- 7. Scheduling thread pool parameter tuning;
- 8. Registry index optimization to alleviate the lock table problem;
- 9. Add Jboot actuator Sample sample project;
- 10. The task list is optimized, and supports filtering tasks according to the attributes of "task status" and "person in charge";
- 11. The task log list interaction is optimized, and the operation buttons are merged into split buttons;
- 12. Project dependencies are upgraded to newer stable versions, such as spring, springboot, groovy, xxl-rpc, etc.; and redundant POMs are cleaned up;
- 13. Upgrade xxl-rpc to a newer version, and fix the problem that the remote service is unavailable when the proxy service is initialized, resulting in the creation of long-term redundant connections;
- 14. The date sorting of the homepage scheduling report is out of order under TIDB;
- 15. The two-way communication timeout between the dispatch center and the actuator is adjusted to 3s;
- 16. The scheduling component destruction process is optimized, first stop the scheduling thread, then wait for the time wheel memory task to be processed, and finally destroy the time wheel thread;
- 17. The executor callback thread is optimized, and the problem of destruction when the callback address is empty is fixed;
- 18. HttpJobHandler is optimized, and the response data specifies UTF-8 format to avoid Chinese garbled characters;
- 19. Code optimization, the ConcurrentHashMap variable type is changed to ConcurrentMap to avoid compatibility issues caused by different implementations of different versions;

### 7.28 Version v2.1.1 Release Notes[2019-11-24]
- 1. Automatic log clearing function of dispatch center (so far, dispatch center/executors support automatic log clearing, and the expiration days are set to 30 days by default): a new configuration item ("xxl.job.logretentiondays") for log retention in dispatch center The number of days, expired logs are automatically cleaned up; solve the problem of slow SQL in the log table in the case of massive logs; it takes effect when the limit is greater than or equal to 7, otherwise the cleanup function is turned off, and the default is 30;
- 2. Scheduling report optimization: Add a log report storage table, and the task logs within three days will be asynchronously synchronized to the report once per minute; the task report only reads the report data, which greatly improves the loading speed;
- 3. Cron online generation tool: Add task, edit box to generate Cron expression online through components;
- 4. Cron's next execution time query: support online viewing of subsequent 5 consecutive execution times through the interface;
- 5. Added the application health check function in the dispatch center, with the help of "spring-boot-starter-actuator", the relative address is "/actuator/health";
- 6. The default encoding of the DB script is changed to utf8mb4, and the character garbled problem is fixed (Mysql version 5.7+ is recommended);
- 7. Tasks in the scheduling center are evenly distributed, and the trigger component acquires tasks related to the number of thread pools each time, avoiding the concentration of a large number of tasks on a single scheduling center cluster node;
- 8. The task trigger component is optimized. The preloading frequency is normally once every 1s. When the preloading bye is active, it will automatically sleep for a loading cycle, and the loading frequency will be dynamically reduced to reduce the DB pressure;
- 9. Scheduling component optimization: Forbid configuration and startup of Cron that will never be triggered; when the task Cron is triggered and will never be triggered after the last trigger, such as a one-time task, actively stop related tasks;
- 10. DB reconnection optimization, fix the problem that task scheduling stops after DB downtime and reconnection, and automatically join the scheduling cluster to trigger task scheduling after reconnection;
- 11. The registration monitoring thread is optimized to reduce the probability of deadlock;
- 12. The scheduling center log deletion optimization is changed to obtain the ID by page and delete according to the ID, so as to avoid the deadlock problem caused by batch deletion of massive logs;
- 13. Fix the problem of parameter loss when the task is retried;
- 14. The scheduling center removes the "now()" function in SQL; the cluster deployment no longer depends on the DB clock, and only needs to ensure that the scheduling center application node clocks are consistent;
- 15. Adjust the loading order of task trigger components to avoid I18N NPE problems caused by random loading order of components in small probability;
- 16. JobThread self-destruction optimization to avoid task loss in triggerQueue caused by concurrent triggering;
- 17. The password of the dispatch center is limited to 18 characters, and the problem of being unable to log in when the password exceeds 18 characters is fixed;
- 18. Fixed the problem of invalid pagination parameters of the task alarm component;
- 19. Upgrade xxl-rpc version: server-side thread optimization, reduce thread memory overhead; IpUtil optimization: increase connectivity check, filter clearly illegal network cards;
- 20. The dispatch center callback API service is changed to restful mode;
- 21. UI optimization, the width ratio of task list and log list data table is adjusted to avoid data wrapping and improve experience;
- 22. The login interface cancels the default login account password;
- 23. Adjust the attributes of the actuator table, adjust the "order" attribute to an integer, and solve the problem that the actuator data cannot be sorted correctly when there are many actuators;
- 24. The interactive optimization of the task list supports viewing the registration node of the executor to which the task belongs;
- 25. Project dependencies are upgraded to newer stable versions, such as spring, spring-boot, mybatis, slf4j, groovy, etc.;
- 26. Log component optimization: the scheduling center supports controlling the maximum number of rows loaded for each request, and requests in batches when the log volume is too large, so as to avoid blocking the page when the log volume is too large for a single load;

### 7.29 Version v2.1.2 Release Notes[2019-12-12]
- 1. Method task support: from the original job development method based on the JobHandler class, it is optimized to support the method-based task development method; therefore, it can support the development of multiple task methods in a single class for class reuse
```
@XxlJob("demoJobHandler")
public ReturnT<String> execute(String param) {
     XxlJobLogger.log("hello world");
     return Return T. SUCCESS;
}
```
- 2. Remove commons-exec and implement it in a native way to reduce third-party dependence;
- 3. Fix the problem of garbled characters in the actuator callback;
- 4. Optimization of dispatcher servlet loading order in dispatching center;
- 5. Actuator callback address https compatible support;
- 6. Multiple projects depend on upgrading to a newer stable version;
- Note: The logic of the latest version "XxlJobSpringExecutor" has been adjusted. For the configuration method of this component in historical projects, please refer to the Sample sample project for adjustments, especially pay attention to the need to remove the init and destroy methods of the component;

### 7.30 Version v2.2.0 Release Notes[2020-04-14]
- 1. RESTful API: The dispatch center and the executor provide language-independent RESTful API services, and any third-party language can connect to the dispatch center or implement the executor.
- 2. Task copy function: click copy to pop up a new task pop-up box, and initialize the copied task information;
- 3. When the task is executed manually once, it is supported to specify the machine address for this execution, if it is empty, it will be obtained from the executor;
- 4. Task result loss processing: if the scheduling record stays in the "running" state for more than 10 minutes, and the corresponding executor heartbeat registration fails and is offline, the local scheduling will be actively marked as failed;
- 5. The dispatch center upgrades springboot2.x; therefore, the system requires JDK8+;
- 6. The XxlJob annotation scanning method is optimized, which supports common situations such as searching for parent classes, interfaces, and class-based agents; repairing the small-probability NPE problem when the task is empty;
- 7. Remove the old class annotation JobHandler. It is recommended to use the method annotation "@XxlJob" for task development; (If you want to keep the class annotation JobHandler usage, you can refer to the old logic custom development);
- 8. Modularization of task alarm components: If you need to add an alarm method, you only need to add an alarm implementation that implements the "com.xxl.job.admin.core.alarm.JobAlarm" interface, which is more flexible and convenient custom made;
- 9. Improve the internationalization of the dispatch center: add support for "Traditional Chinese". The default is "zh_CN"/Simplified Chinese, the optional range is "zh_CN"/Simplified Chinese, "zh_TC"/Traditional Chinese and "en"/English;
- 10. Optimization of executor registration logic: add a new configuration item "registration address / xxl.job.executor.address", use this configuration as the registration address first, and use the embedded service "IP:PORT" as the registration address when it is empty. In this way, it supports the dynamic IP and dynamic mapping port issues of container type executors more flexibly.
- 11. The default database connection pool is adjusted to hikari, and the tomcat-jdbc dependency is removed;
- 12. Multiple projects rely on upgrading to a newer stable version, such as mybatis, groovy and mysql drivers, etc.;
- 13. Optimized the graceful shutdown of the executor, and fixed the problem that the task thread was interrupted and did not join, resulting in the loss of the callback;
- 14. Consistent hash routing strategy optimization: the default number of virtual nodes is adjusted to 100 to improve the balance of routing;
- 15. General HTTP task Handler (httpJobHandler) optimization, extended custom parameter information, sample parameters are as follows;
```
url: http://www.xxx.com
method: get or post
data: post-data
```
- 16. The SQL script code is executed in utf8mb4 by default, avoiding garbled characters in the container environment with a small probability;
- 17. Web IDE interaction problem repair: After entering the source code comment, press Enter to jump to the error problem;
- 18. Optimization of executor initialization logic: fix the problem that lazy-loaded beans are initialized in advance;
- 19. Optimized the default value of actuator registration;
- 20. Fix bootstrap.min.css.map 404 problem;
- 21. Optimize UI interaction of actuator, remove redundant order attribute;
- 22. Implement the length limit of the remark message, and fix the problem that the data is too long and cannot be stored, which leads to the failure of the callback;
Note: Adjust the individual fields of the XxlJobSpringExecutor component: "appName" is adjusted to "appname", and you need to pay attention when upgrading this component;   

### 7.31 Version v2.3.0 Release Notes[2021-02-09]
- 1. [New] Scheduling expiration strategy: the compensation processing strategy for the dispatch center to miss the dispatch time, including: ignore, immediately compensate and trigger once, etc.;
- 2. [New] trigger strategy: In addition to the regular Cron, API, and parent-child task trigger methods, a new trigger method of "fixed interval trigger, (fixed delay trigger, in the experiment)" is added;
- 3. [New] Newly added task assistance tool "XxlJobHelper": Provide unified task assistance capabilities, including: task context information maintenance and acquisition (task parameters, task ID, fragmentation parameters), log output, task result settings...etc. ;
     - 3.1, "ShardingUtil" component obsolete: use "XxlJobHelper.getShardIndex()/getShardTotal();" to get sharding parameters;
     - 3.2, "XxlJobLogger" component obsolete: use "XxlJobHelper.log" for log output;
- 4. [Optimization] The "execute" method of the task core class "IJobHandler" cancels the entry and exit parameter design. Instead, use "XxlJobHelper.getJobParam" to obtain task parameters and substitute method input parameters, and use "XxlJobHelper.handleSuccess/handleFail" to set task results and substitute method output parameters. The sample code is as follows;
```
@XxlJob("demoJobHandler")
public void execute() {
   String param = XxlJobHelper.getJobParam(); // get parameters
   XxlJobHelper.handleSuccess(); // Set task result
}
```
- 5. [Optimization] Cron editor enhancement: When the Cron editor modifies cron, you can view the latest running time in real time;
- 6. 【Optimization】Actuator sample project specification arrangement;
- 7. [Optimization] Task scheduling lifecycle refactoring: schedule, trigger, handle, callback, complete;
- 8. [Optimization] Actuator registration component optimization: the registration logic is adjusted to asynchronous mode to improve registration performance;
- 9. [Optimization] Actuator authentication verification: Actively verify the accessToken when the actuator is started, and actively warn if it is empty; (planned security enhancement: AccessToken dynamic generation, dynamic start and stop, etc.)
- 10. [Optimization] Mailbox alarm configuration optimization: separate the "spring.mail.from" and "spring.mail.username" attributes, and more flexibly support some password-free email services;
- 11. [Optimization] Multiple projects depend on upgrading to a newer stable version, such as netty, groovy, spring, springboot, mybatis, etc.;
- 12. [Optimization] UI components are routinely upgraded to improve component stability;
- 13. [Optimization] Interactive optimization of the scheduling center page: cancel the password column in the user management module; cancel autocomplete in multiple places; XSS interception verification in the actuator management module, etc.;
- 14. [Optimization] Optimization of slow SQL problem in dispatching center task status detection;
- 15. [Fix] GLUE-Java mode tasks, init/destroy cannot execute the problem;
- 16. [Fix] Cron editor problem fix: Fix the problem that other fields will be reset when a single field of cron is modified in a small probability;
- 17. [Fix] General HTTP task Handler (httpJobHandler) optimization: fix "setDoOutput(true)" that causes task request GetMethod to fail;
- 18. [Fix] Optimize the commandhandler sample task of the executor, and fix the script process hang problem in extreme cases;
- 19. [Fix] Optimizing the scheduling communication components, and repairing the failure of heartbeat detection when calling the DotNet version executor in RestFul mode;
- 20. [Repair] Fix the problem of garbled characters in the dispatching center's remote execution log query;
- 21. [Repair] Optimized the loading order of dispatching center components, and repaired the scheduling failure problem caused by the initial slowness of dispatching components in extreme cases;
- 22. [Fix] Optimize the executor registration thread, and fix the NPE problem caused by initialization failure in extreme cases;
- 23. [Repair] Scheduling thread connection pool optimization, repair connection validity check timeout problem;
- 24. [Fix] Optimize the executor registry field to solve the problem that too many executor registration nodes lead to registration information storage and update failure;
- 25. [Repair] Optimized the routing strategy of rotation training, and fixed the concurrency problem under small probability;
- 26. [Fix] Fix the problem that https changes to http after page redirection;
- 27. [Repair] Optimized the cleaning of the executor log, and repaired the abnormal problem caused by the log file being empty in a small probability;

### 7.32 Version v2.3.1 Release Notes[2022-05-21]
- 1. [Repair] Fix risk vulnerabilities and upgrade project dependencies of lower versions: CVE-2021-2471, CVE-2022-22965, etc.
- 2. [Repair] Repair the failure alarm logic, and transfer the mailbox verification logic to EmailJobAlarm to avoid interference with other alarm methods.
- 3. [Optimization] AccessToken is enabled by default for scheduling communication to improve system security (it is recommended to customize accessToken in the production environment).
- 4. [Optimization] Merge multiple PRs, project code structure, robustness optimization: PR-2833, PR-2812, PR-2541, PR-2537, PR-2514, PR-2509, PR-2591.
- 5. [Optimization] Optimize the task thread name to improve readability and problem location efficiency (ISSUE-2527).

### 7.33 Version v2.4.0 Release Notes[2023-03-23]
- 1. [Optimization] Bean scanning logic optimization for executor tasks: solve the problem of lazy loading annotation failure.
- 2. [Optimization] Multiple projects rely on upgrading to a newer stable version, involving netty, groovy, spring, springboot, mybatis, etc.;
- 3. [Repair] "CVE-2022-36157" authorization vulnerability repair.
- 4. [Repair] "CVE-2022-43183" SSRF vulnerability repair.

### 7.34 Version v2.4.1 Release Notes[Planning]
- 1. [Optimization] [Planning] Reconstruction of task log: only one main task is recorded in one scheduling, and the start and end time and status are maintained.
     - Normal task: only record one main task;
     - Broadcast task: record a main task, and record a sub-task for each shard task, which is associated with the main task;
     - Retry missions: when failed, add main missions. All scheduling records, including entry scheduling and retry scheduling, are mounted on the main task.
- 2. [Optimization] [Planning] Fragmentation tasks: After all tasks are completed, the rear nodes will be dispatched;

### 7.35 new version planning [planning]
- 1. [Planning] DAG process tasks
     - DAG task: support parameter transfer, share data: create and manage DAG task, view and operate DAG task log;
     - Subtask: Abandoned
- 2. [Planning] Multi-database support, the DAO layer is implemented through JPA, and the database type is not limited;
- 3. [Planning] Alarm enhancement: email alarm + webhook alarm;
- 4. [Planning] Security enhancement: AccessToken dynamic generation, dynamic start and stop; control scheduling, callback;
- 5. [Planning] task import and export tool, which flexibly supports scenarios such as version upgrades and migrations.


###TODO LIST
- 1. Task sharding routing: The sharding uses the consistent Hash algorithm to calculate the sharding sequence as stable as possible. Even if the registration machine fluctuates, it will not cause large fluctuations in the batch sharding sequence; currently, IP natural sorting is used, which can meet demand, to be determined;
- 2. Scheduling isolation: the scheduling center maintains different scheduling and remote triggering components for different actuators.
- 3. Scheduling task priority;
- 4. Multi-database support, the DAO layer is implemented through JPA, and the database type is not limited;
- 5. Executor Log cleaning function: When the dispatch center Log is deleted, the Log file in the executor is deleted synchronously;
- 6. Delayed tasks: triggered by API, support "dynamic parameter transfer, delayed consumption"; this function conflicts with XXL-MQ, and the latter is recommended for this scenario;
- 7. The scheduling thread pool is changed to a coroutine method, which greatly reduces the system memory consumption;
- 8. Full local cache of task and executor data; new message table broadcast notification;
- 9. Busy transfer optimization, when all machines are busy, they will no longer fail directly;
- 10. Optimization of task trigger parameters: support selection of "Cron trigger", "Fixed interval trigger", "Specified time point trigger", "No selection", etc.;
- 11. Schedule log list plus execution time column, and support sorting;
- 12. DAG process tasks:
     - Replace subtasks, support parameter passing, share data:
     - Configure parallel "a-b, b-c" path lists to form serial, parallel, dag task processes, "dagre-d3" drawing; task dependencies, flowcharts, subtasks + countersigned tasks, and logs of each node; support based on success and failure select branch;
     - Fragmentation tasks: After all tasks are completed, the subsequent nodes will be dispatched;
- 13. Date filtering: support multiple time period exclusions;
- 14. Alarm enhancement:
     - Email alert: support custom title, template format;
     - webhook alarm: support custom alarm URL, request body format;
- 15. Added task operation mode "GLUE mode (GO)" to support GO tasks;
- 16. Web Ide version comparison function in GLUE mode;
- 17. Registration center optimization, real-time registration discovery: the heartbeat registration interval is 10s, if the refresh fails, the registration information will be registered for the first time and the registration information will be updated immediately, similar to the heartbeat; 30s expired and destroyed;
- 18. Provide the Docker image of the executor;
- 19. Script tasks support data parameters. The new version only supports single parameters and does not support compatibility;
- 20. Batch scheduling: Scheduling requests enter the queue, scheduling threads obtain scheduling requests in batches and initiate remote scheduling; improve thread efficiency;
- 21. Executor ports are multiplexed, and multiplexed container ports provide communication services;
- 22. Sub-tasks are triggered after all shard tasks are successful;
- 23. New executor description attribute; task name attribute;
- 24. Custom failure retry interval;
- 25. Task label: easy to search;
- 26. Actuator: dag executor, no need to register the machine;


## 8. Others

### 8.1 Project Contribution
Welcome to contribute to the project! For example, submit a PR to fix a bug, or create a new [Issue](https://github.com/xuxueli/xxl-job/issues/) to discuss new features or changes.

### 8.2 User Access Registration
More connected companies are welcome to register at [registration address](https://github.com/xuxueli/xxl-job/issues/1), registration is only for product promotion.

### 8.3 Open source agreement and copyright
The product is open source and free, and will continue to provide free community technical support. It can be freely accessed and used by individuals or enterprises. If necessary, you can contact the author by email to obtain project authorization for free.

- Licensed under the GNU General Public License (GPL) v3.
- Copyright (c) 2015-present, xuxueli.

---
### Donate
No matter how much the donation amount is enough to express your heart, thank you very much :) [Go to Donate](https://www.xuxueli.com/page/donate.html )