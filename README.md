MoreEpochs mod v2.2 by JustAMiner.
***********************************

Default Claymore ETH Miner v15.0 only supports up to 384 DAG epoch, and
the miner stopped working already. MoreEpochs mod adds support of DAG 
epochs up to 500 so you can continue to use legendary Claymore ETH miner!

Currently this mod supports only Windows version of the miner, Nvidia GPUs 
with at least 6 GB of video memory, and several AMD GPUs with at least 8 GB 
of video memory: Polaris RX 470,480,570,580,590, Navi RX 5500XT, 5600, 5600XT,
5700, 5700XT, Vega. Please read "AMD GPUs support" section below for details.

The mod also fixes bugs of the original miner and adds new features:

Added features:
---------------

~ command line option "-strap" now works for AMD Polaris GPUs on video drivers 20.5.1+,
  that allows the mod to outperform any other miners for Polaris GPUs.

~ now miner supports Nvidia drivers 460.89+ and initializes NVML properly 
  with these drivers, so temperature monitoring, fan control and power draw
  stats are available.

~ now miner shows AMD GPUs power draw stat on newer AMD drivers (tested with 20.12.1).

~ now miner shows AMD driver version at startup and warns if driver's version is not
  supported.

~ now miner saves AMD Polaris GPUs' core and memory clocks/voltages at startup (before
  applying custom ones with -cclock,-mclock,-cvddc,-mvdcc) and restores it during exit.


Fixed bugs of the original miner:
---------------------------------

~ miner was unable to access nvml.dll on Windows 10, so temperature
  monitoring, fan control and power draw stats were unavailable.

~ miner was unable to apply core clocks from -cclock to Navi GPUs on new video drivers.




DOWNLOAD LINK:
**************

https://github.com/just-a-miner/moreepochs/releases



HOW TO USE:
***********

Unpack the archive and run the miner as you usually do. If the mod will
complete its job successfully, you will see green colored message below 
Claymore's logo:

 ******************************************************************
 *               MoreEpochs mod v2.2 by JustAMiner                *
 *                    justaminer@tutanota.com                     *
 *       https://bitcointalk.org/index.php?topic=5305046.0        *
 ******************************************************************

and now the miner is able to work with DAG epochs up to 500.

If you don't see this message, make sure you are using my original mod from
my download link. If it still doesn't work for you, contact me and I will 
try to help you.



AMD GPUs support:
*****************

Drivers:
--------

You should use AMD video driver 20.5.1 or newer (most tests were done on
driver 20.12.1), because older drivers can't allocate 4+ GB video buffer
as single piece and that will prevent the miner from creating 4+ GB DAG.


Issues:
-------

- 8 GB R9 390 doesn't work.

This issue can be fixed in next versions of the mod. 


List of working GPUs:
---------------------

AMD GPUs that work fine (tested on AMD video driver 20.12.1)

- 8 GB AMD Polaris: RX 470, 480, 570, 580, 590
- 8 GB AMD Navi: RX 5500XT, 5600, 5600XT, 5700, 5700XT
- 8+ GB AMD Vega GPUs


"-strap" and "-rxboost" options:
--------------------------------

Command line options "-rxboost" and "-strap" (since v2.0 of the mod)
works with AMD Polaris GPUs on video drivers 20.5.1+ (tested on AMD video 
drivers 20.5.1 and 20.12.1). These options apply fast memory timings and 
greatly increase mining speed. 
If you are going to use these options first time, you will need to do next
steps once:

1) run miner as administrator once with "-rxboost 1" option. Miner should
automatically uninstall old strap driver and install new one. If miner
was unable to do auto uninstall/install of new strap driver, see step 2) and 3).

2) in miner folder go to "\strap_driver" subfolder and run as 
admin "uninstall_strap_driver.cmd". This will stop and uninstall old strap
driver if it was installed.

3) run miner as admin with "-driver install" option.

If miner successfully installed new strap driver, you will see next messages:

 'Driver installed successfully.'

After that you don't need to run miner as administrator anymore and you can
use -rxboost and -strap options.

Note that rxboost/straps now apply after DAG generation to avoid possible
DAG corruption. When DAG generation is finished and if rxboost/strap applied
successfully, you will see next green colored messages :

 'GPU #x strap "..." is applied successfully'
 'GPU #x -rxboost option is applied successfully'

where x is GPU index that rxboost/strap applied to and "..." is specific strap.


Be aware, that some software can prevent straps from working. For example tool
named "HwInfo" does that, if you started it once, straps won't have effect
on mining speed until you reboot your rig. Also make sure that you didn't
set manual memory timings in AMD Radeon Software, this also doesn't allow
straps to work.


Please note that both -rxboost and -strap can crash/freeze your rig because
not every GPU is able to work with faster timings especially at high memory
clocks. Refer to "Readme!!!.txt" to get more information about how to use -strap 
and -rxboost.


Compute Mode:
-------------

If after installing new AMD driver your AMD GPUs hash at very low speed, e.g. 
RX 580 shows like 9 MH/s instead of 27-33 MH/s, you need to enable Compute Mode 
in AMD Drivers. To do this, you need to run the miner as administrator once and 
after you see message:

 'Press "y" to set Compute Mode and disable CrossFire in AMD drivers for all cards'

press y key. After that you should see next message:

 'All AMD cards use Compute Mode now, please reboot the system to apply it'.

Exit the miner and reboot your rig. Now you can run miner as usual and your
AMD GPUs should work at full speed.



CUDA 8 AND 10:
**************

By default, there is Cuda 8 vesion of file 'EthDcrMiner64.exe' in the root
folder of the miner. If you want to use Cuda 10 version of Claymore ETH Miner
 (it can give some speed increase), copy 'cudart64_100.dll' and 
'EthDcrMiner64.exe' from the 'cuda 10' subfolder to the root folder of the 
miner and overwrite 'EthDcrMiner64.exe' there.

Then you can run the miner as usual and you should see:

 CUDA Driver Version/Runtime Version: xx.x/10.0

As you can see, Runtime Version is 10.0. It means miner uses Cuda 10.0 API.

If you want to get back to Cuda 8, unpack file 'EthDcrMiner64.exe' from the 
mod's archive root folder, and copy it to the root folder of the miner, 
overwriting 'EthDcrMiner64.exe' there. 

After that if you'll run the miner you should see:

 CUDA Driver Version/Runtime Version: xx.x/8.0

As you can see, Runtime Version is 8.0. It means miner uses Cuda 8.0 API.

Cuda 8 can be slightly faster on some rigs, and Cuda 10 can be slightly faster
on others. You can test both versions on your rig and choose fastest one.



FUTURE PLANS:
*************

Feature versions of this mod will have support of Linux version of the miner.



CONTACTS:
*********

Bitcointalk.org: https://bitcointalk.org/index.php?topic=5305046.0

Email: justaminer@tutanota.com



MOD VERSION HISTORY:
********************

v2.2
----------------

- Now miner saves AMD Polaris GPUs' core and memory clocks/voltages at startup (before applying custom ones with -cclock,-mclock,-cvddc,-mvdcc)
  and restores it during exit.

- Now miner shows AMD driver version at startup and warns if it's not supported.

- Fixed bug of original miner with applying -cclock values to Navi GPUs on new video drivers.

- Several minor fixes.


v2.1
----------------

- Changed behavior of "-driver uninstall" option. By default, miner also tries to disable testsigning mode during strap driver uninstall. This
  often leads to error on systems with SecureBoot enabled and prevents miner from uninstalling strap driver. Now when miner started with 
  "-driver uninstall" option, it only uninstalls strap driver without trying to disable testsigning mode. 

- Command line option "-mode" now has default value of 1, which means that if this option is not specified, dual-mining mode is disabled by default
  and miner works in ETH-only mining mode. This is usefull for AMD GPUs (Polaris), because allow miner to get best mining speed by either automatic or
  manual fine-tuning of -dcri values.

- Added messages that straps/rxboost will be applied after DAG generation if strap/rxboost options used. Remade several messages that miner 
  displays in case of error during installing/uninstalling strap driver to give user more clear instructions.

- Several small fixes.


v2.0
----------------

- Command line option "-strap" now works for AMD Polaris GPUs with video drivers 20.5.1+ (most tests were done on 20.5.1 and 20.12.1).
  Read "AMD GPUs support" section for details.


v1.9
----------------

- Fixed issue with incorrect shares on 8+ GB Vega AMD GPUs.


v1.8
----------------

- Fixed issue with incorrect shares on 8 GB Polaris AMD GPUs: RX 470, 480, 570, 580 (tested on AMD video driver 20.12.1).

- Command line option "-rxboost 1" works fine with Polaris AMD GPUs (tested on AMD video driver 20.12.1).
  For now avoid using "-strap" command line option for AMD GPUs, it will crash rig. This problem will be fixed in 
  next versions of the mod.


v1.7
----------------

- now miner shows AMD GPUs power draw stats on newer AMD drivers (tested on AMD video driver 20.12.1).


v1.6
----------------

- Improved devfee connection handling. Reduced retry delay to 1 second between connection attempts to other devfee pools
  if miner can't connect to default devfee pool when devfee starts. Reduced retry delay to 1 second between connection 
  attempts to other devfee pools if miner lost connection to devfee pool during mining devfee.

- several minor bug fixes and improvements


v1.5
----------------

- Fixed issue with incorrect shares on Navi AMD GPUs.


v1.4
----------------

- Added support for Nvidia drivers 460.89+, now the miner initializes NVML properly with these drivers,
  so temperature monitoring, fan control and power draw stats are available.


v1.3
----------------

- Fixed Claymore's bug that lead to error "NVIDIA NVML library not found, temperature monitoring for NVIDIA GPUs disabled." on
  Windows 10. Nvidia driver 456.71 is tested on Windows 10 and shows temperature, fan speed, power draw of Nvidia GPUSs, and
  allow to control GPUs fans. Nvidia driver 460.89 still gives the error "NVML API: Init Error 1" - this will be fixed in 
  next releases of the mod.


v1.2
----------------

- Several AMD GPUs are now enabled to work with DAG epochs 385+ :
  R470/R480, Vega, Navi. This is test support, please report
  any problems.


v1.1
----------------

- added support of Cuda 10 EthDcrMiner64.exe
- fixed bug with buffer allocation for DAG epochs 388+


v1.0
----------------

- First version, supports only Cuda 8 EthDcrMiner64.exe and Nvidia GPUs
