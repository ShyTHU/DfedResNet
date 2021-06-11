# DfedResNet
A Doubly Fed Cross-Residual Deep Neural Network for High-Precision Magnetic Flux Leakage Defect Size Estimation

Please note that this code is derived from an unpublished paper, so it is for reviewers only, that is, only reviewers can get the password of the dataset, but the code is public to everyone.
If the paper is accepted, we will publish the data set. Everyone is welcome to read the paper and use our code and data.

Paper Portal: However, not publish.

Author:      Hongyu Sun

Affiliation: Tsinghua University

Email:     sunhy18@mails.tsinghua.edu.cn

Abstract of our paper:

Defect depth is an important indicator for magnetic flux leakage (MFL) detection and estimation, in which the quantization error for defect depth is closely related to the length and width errors, but this feature has not been introduced into deep learning (DL) based defect quantification algorithms. Therefore, the network’s performance has always been limited because the training logic is different from the theoretical explanation of the quantification process. Here in this work, to describe and integrate the above theory in a deep neural network, we propose a doubly fed cross-residual network (DfedResNet) suitable for MFL defect detection based on DL. DfedResNet is used to quantify defects in MFL data and can automatically extract deep features of defects and is proven to be able to effectively achieve high-precision quantification of defect length, width, and depth simultaneously, especially the defect depth. Moreover, data from all three dimensions are effectively used for network training, and the originally measured magnetic signal data are used in place of recognized images to avoid the loss of defect information and further improve the quantification accuracy. The results show that the deep DfedResNet model proposed in this paper exhibits high quantitative performance compared with other network structures and traditional algorithms.
Note: There are some differences between the paper and the code, which is caused by the revision during the review process. The additional code is as follows:

    def hybrid_loss_L(y_true, y_pred): # Add the traditional loss function term to the physical inspired loss term

        lmd_phys = 0.5 # Indicates the degree of introduction of physical concepts
        y_true = tf.cast(y_true[:, 0], dtype=tf.float32)
        loss_cus = tf.reduce_mean(tf.square(y_pred[:, 0] - y_true))
        loss_phys_L = tf.reduce_mean(tf.square(y_pred[:, 0] - tf.cast(l_phys, dtype=tf.float32)))
        total_loss_L = loss_cus + lmd_phys * loss_phys_L

        return total_loss_L

    def hybrid_loss_W(y_true, y_pred):

        lmd_phys = 0.5
        y_true = tf.cast(y_true[:, 0], dtype=tf.float32)
        loss_cus = tf.reduce_mean(tf.square(y_pred[:, 0] - y_true))
        loss_phys_W = tf.reduce_mean(tf.square(y_pred[:, 0] - tf.cast(w_phys, dtype=tf.float32)))
        total_loss_W = loss_cus + lmd_phys * loss_phys_W

        return total_loss_W
