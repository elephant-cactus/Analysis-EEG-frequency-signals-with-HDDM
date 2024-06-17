# analysis-EEG-frequency-signals-with-HDDM
提取EEG频段能量进行漂移扩散建模

这个项目演示了一种提取EEG特定频段能量进行漂移扩散建模建模的方法。

在二分类恐惧泛化决策任务中，使用了E-prime与Neuroscan采集了4名被试的行为数据与EEG脑电信号（有效通道 = 60）。

将E-prime行为数据整理为‘eprime_data.csv’文件，这个文件包含了所有被试的行为数据（每一行是一个trial）。

使用Matlab的EEGLAB扩展对每个被试的脑电信号进行预处理（预处理的流程写在了‘EEG_preprocessing.mlx’中）；

预处理后的文件使用‘TFA_hddm.mlx’脚本进行了短时傅里叶变换，为每个被试生成两个4D-single的mat对象用于存放每个trial（epoch）上的能量信息（基线矫正前：P_data、基线校正后：P_BC，形状：chan*fre*time*epoch）；

‘TFA_hddm.mlx’还用于计算P_data、P_BC对象中特定频段（alpha、beta、theta、delta）在每个电极、特定时间段，每个epoch（trial）上的能量大小（微伏平方），并将他们写成trial-wise的csv文件，在这个例子中，我提取了alpha和beta波；

‘TFA_hddm.mlx’还用于将记载了行为数据与上述频段能量数据的csv文件合并，得到‘combined_data’；

‘hddm_modeling.ipynb’对‘combined_data’中的数据进行了建模，分析了Fpz电极点上的alpha能量与决策阈限（参数a）在不同确定性刺激上的关系，以及状态焦虑分数对这种关系的调节作用。



This project demonstrates a method for extracting specific EEG band energies and using them for drift diffusion modeling.

In a binary classification fear generalization decision task, behavioral data and EEG signals from four participants were collected using E-prime and Neuroscan (effective channels = 60).

The behavioral data from E-prime were organized into a file named 'eprime_data.csv', which contains all participants' behavioral data (each row represents a trial).

The EEG signals for each participant were preprocessed using Matlab's EEGLAB extension (the preprocessing steps are detailed in 'EEG_preprocessing.mlx').

The preprocessed files underwent short-time Fourier transform using the 'TFA_hddm.mlx' script. This generated two 4D-single mat objects for each participant, used to store energy information for each trial (epoch) (before baseline correction: P_data; after baseline correction: P_BC, shape: chan*fre*time*epoch).

The 'TFA_hddm.mlx' script also calculated the energy levels (in microvolt squared) in specific frequency bands (alpha, beta, theta, delta) at each electrode and specific time segment for each epoch (trial), and wrote these into trial-wise CSV files. In this example, alpha and beta waves were extracted.

Additionally, 'TFA_hddm.mlx' was used to merge the behavioral data and the energy data from the specified frequency bands into a 'combined_data' file.

The 'hddm_modeling.ipynb' notebook then modeled the data from 'combined_data', analyzing the relationship between alpha energy at the Fpz electrode and decision thresholds (parameter a) under different certainty stimuli, as well as the moderating effect of state anxiety scores on this relationship.
