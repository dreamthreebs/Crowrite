# 251016-effective beam

设想天空上有一个平滑的大尺度亮度梯度；\
仪器的波束是椭圆形的，并且随着扫描方向不断旋转。\
当它沿不同方向扫描时，每一次的“拉伸方向”不同，\
于是本应光滑的梯度在合成图像中被切割成细条纹——这些条纹对应高ℓ 模式。\
因此看起来像是大尺度功率“泄漏”到了小尺度。



If the scan is along the minor axis of the ellipse, repeated hits in a pixel will tend to make the effective beam more symmetric than the true beam, hence the final map will have less severe high resolution systematics. On the other hand, if the scan is along the major axis, the elongation will be enhanced in the effective beam and the final map will have more high resolution systematics.
