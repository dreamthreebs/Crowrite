# 1105-inpainting steps

1. &#x20;do zzr EB leakage correction(with point sources and edges being 1.5 disc region masked.), then inpaint on B with m3 and m2 methods(but with wider 1.8 disc region).
2. &#x20;do zzr EB leakage correction (without point sources but with edges), then add 1.8 disc region mask. inpaint direct on B maps with m3 and m2 methods.
