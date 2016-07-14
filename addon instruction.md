#Staubli robot addon 介绍

##Expasion
* num $getState():返回RSI板上七段显示管显示的系统状态。
* bool $delete(string sPath):删除指定文件或文件夹。
* bool $copy(string sFrom,string sTo):把文件或文件夹从sFrom复制到sTo。
* bool $rename(string sFrom,string sTo):把文件或文件夹从sFrom移动到sTo。
* bool $fileExits(string sPath):判断指定的文件是否存在，sPath是文件路径。
* bool $fileOpen(string sPath,string sMode):以读或写的方式打开一个文件。最多同时打开10个文件。
* num $fileGet(num nFileHandler,string& sLine[],num nNbLines):读取nNbLines行，储存在sLine中，返回读取的`有效`行数
* num $fileGet(num nFileHandler,num& nBytes[],num nNbytes):读取nNbytes个字符，储存在nBytes中，返回读取的`有效`字符数。
* num $fileSet(num nFileHandler, string sLines[], num nNbLines)：从sLines中取nNbLines个字符串写入文件中，返回实际写入的数目。
* num $fileSet(num nFileHandler, num nBytes[], num nNbBytes):从nBytes中取nNbBytes个字符写入文件中，返回实际写入的数目。
* bool $fileClose(num nFileHandler):关闭由文件指针nFileHandler指向的文件。打开的文件不会自动关闭。
* num $getPowerCOunt():返回机器人总上电时间，单位小时。
* num $getFreeSpace(x_sPart):获取分区剩余空间，x_sPart:“/sys”,“/usr”,“/log”。
* num $circleFind(point& pPointsIn[], frame& fFrameOut, num& nRadiusOut):
获取通过输入点（pPointsIn[]）的一个圆。
pPointsIn:输入点，至少3个点，最多10个点；
fFrameOut:圆所在的坐标系，其原点即圆的中心点；
nRadiusOut:圆的半径；
返回值：圆与输入点的误差。
* bool $setArmLimits(joint jMin,joint jMax):设置手臂限位
* bool $setCellLimits(joint jMin,joint jMax)：设置单元限位

##Motion
* num $rotAngle(trsf tTransformation):返回一个变换trsf的等效转角。
* num $getRot(trsf tTransformation,num& nXaxis,num& Yaxis,num& nZaxis)
返回一个变换trsf的等效轴和等效转角。等效轴是一个单位向量。
* trsf $setRot(num nAngle,num& nXaxis,num& nYaxis,num& nZaxis)
由等效转角和等效轴计算一个变换。
* ponit $getPosFbK(tool tTool,frame fReference):获取由编码器计算得到的位置。
* joint $getJntFbk():获取由编码器得到的关节位置。
* void $computeJntFrc(joint jPosition, num& nVelocity[], num& nAcceleration[], num& nForce[]):计算理论关节力。
* void $externalForce(joint jPosition, tool tTool, num& nJointOverForce[], num&nCartForce[]):计算机器人受到的外部力，等效于TCP中心点。
* num $getCycleTime():计算控制器的系统运行周期。
* num $motionState():返回运动状态。它是以16bits表示的。


##Recorder
* $recClean(string sRecorder):清除指定的recorder（“c”或“d”）。
* $recAdd(string sRecorder,string sVariable):把recorder变量放入recocder列表中，以便记录信息。
* recSize(string sRecorder,num bufferSize):设置sRecorder指定的缓存大小（bytes）。
* recStart(string sRecorder,num  duration,num frequency):使用sRecorder指定的记录器开始记录数据，持续时间duration,采样频率frequency。
* recStop(string sRecorder):停止记录。
* recStore(string sRecorder,string path):把指定的记录器中数据保存在由“path”指定的文件（包含路径）。格式有ctt和txt。


##Velocity
* void $velFrame(frame fReference, tool tTool, mdesc mDesc):  
以fReference为参考设定笛卡尔空间中的速度控制。机器人的运动方向参考fReference(x,y,z,rx,ry,rz)。
* void $velJoint(tool tTool, mdesc mDesc):设置关节模式的速度控制。
* void $velTool(tool, mdesc):设置工具模式的速度控制
* void $setVelCmd(num cmd[6]):设置运动速度。  
**使用：先设置模式，再设置速度。**


