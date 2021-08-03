---
layout: page
title: CoEx 
description: "Correlate-and-Excite: Real-Time Stereo Matching via Guided Cost Volume Excitation"
img: /assets/img/publications/2021_iros_lignet.gif
importance: 1
category: Research
---

<p align="center">
  <img width="422" height="223" src="/assets/img/publications/CoEx/teaser.png">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;">
D1-all% error on KITTI stereo 2015 leaderboard vs. frame rate. Our proposed method CoEx, shown in the red star, achieve competitive performance compared to other state-of-the-art models while also being real-time.</p>
</p>

## Abstract

<span style="font-size:0.9em;">
Volumetric deep learning approach towards stereo
matching aggregates a cost volume computed from input left
and right images using 3D convolutions. Recent works showed
that utilization of extracted image features and a spatially
varying cost volume aggregation complements 3D convolutions.
However, existing methods with spatially varying operations
are complex, cost considerable computation time, and cause
memory consumption to increase. In this work, we construct
[Guided Cost volume Excitation (GCE)](#gce) and show that simple channel excitation of cost volume guided by image can
improve performance considerably. Moreover, we propose a
novel method of using [top-k](#top-k-soft-argmin-disparity-regression) selection prior to soft-argmin
disparity regression for computing the final disparity estimate.
Combining our novel contributions, we present an end-to-end
network that we call [Correlate-and-Excite (CoEx)](#coex-overall-architecture). Extensive
experiments of our model on the SceneFlow, KITTI 2012,
and KITTI 2015 datasets demonstrate the effectiveness and
efficiency of our model and show that our model outperforms
other speed-based algorithms while also being competitive to
other state-of-the-art algorithms
</span>

## Contributions

- <span style="font-size:0.9em;">We present Guided Cost volume Excitation (GCE) to utilize extracted feature map from image as guidance for cost aggregation to improve performance.</span>
- <span style="font-size:0.9em;">We propose a new method of disparity regression in place of soft-argmax(argmin) to compute disparity from the top-k matching cost values and show that it reliably improves performance.</span>
- <span style="font-size:0.9em;">Through these methods, we build a real-time stereo matching network CoEx, that outperforms other speedoriented methods and shows its competitiveness when compared to state-of-the-art models.</span>

## CoEx overall architecture

<p align="center">
  <img width="772" height="231" src="/assets/img/publications/CoEx/coex_overall.png" title="CoEx overall architecture">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;"></p>
</p>

### GCE

<span style="font-size:1em;"> GCE excites stereo cost volume using weights extracted from image features. </span>

<!-- <div class="row">
    <div class="col-sm mt-4 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/exc_0_2b.png' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-4 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/exc_1_2b.png' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-4 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/exc_2_2b.png' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-4 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/exc_3_2b.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>  -->

<!-- <div class="row">
    <div class="col-sm mt-1 mt-md-0" align="center" >
        <img class="img-fluid rounded z-depth-0" width="467" height="562"  src="{{ '/assets/img/publications/CoEx/exc.jpg' | relative_url }}" alt="" title="gce"/>
    </div>
</div>   -->

<p align="center">
  <img width="467" height="562" src="/assets/img/publications/CoEx/exc.jpg" title="GCE excitation weights">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;" markdown="1">
Computed excitation weights in one of the GCE layers. 
  </p>
</p>

<br>

### Top-k soft-argmin disparity regression

<span style="font-size:1em;"> Instead of computing disparity by soft-argmin using the whole cost volume, only the top-k relevant values are used. </span>

<p align="center">
  <img width="747" height="182" src="/assets/img/publications/CoEx/topk_chart.png" title="top-k charts">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;" markdown="1">
Ground truth disparity is represented by vertical solid green line. Predicted disparity is vertical dashed red line. *k=2* makes the closest regression estimates to the ground truth.
  </p>
</p>

## Demo

### Real-time stereo matching

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/coex_compress.gif' | relative_url }}" alt="" title="CoEx"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/psm_compress.gif' | relative_url }}" alt="" title="PSMNet"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-0" src="{{ '/assets/img/publications/CoEx/ganet_compress.gif' | relative_url }}" alt="" title="GANet"/>
    </div>
</div> 
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0" align="center">
        <p>CoEx (Ours)</p>
    </div>
    <div class="col-sm mt-3 mt-md-0" align="center">
        <a href="https://openaccess.thecvf.com/content_cvpr_2018/papers/Chang_Pyramid_Stereo_Matching_CVPR_2018_paper.pdf">
            <span style="color:blue">PSMNet</span>
        </a>
        [1]
    </div>
    <div class="col-sm mt-3 mt-md-0" align="center">
        <a href="https://openaccess.thecvf.com/content_CVPR_2019/papers/Zhang_GA-Net_Guided_Aggregation_Net_for_End-To-End_Stereo_Matching_CVPR_2019_paper.pdf">
            <span style="color:blue">GANet</span>
        </a>
        [2]
    </div>
</div> 
<div class="caption">
    Speed comparison with previous works. *The shown images are compressed, so image quality may not reflect the real output of the models
</div>

### Stereo 3D reconstruction

<p align="center">
  <img width="640" height="336" src="/assets/img/publications/CoEx/recons_compress.gif" title="3d reconstruction">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;" markdown="1">
Reconstructed 3d point cloud computed from the predicted stereo disparity map
  </p>
</p>

### Application - visual odometry and point cloud mapping

<p align="center">
  <img width="640" height="336" src="/assets/img/publications/CoEx/vo+map_compress.gif" title="vo+map">
  <p style="margin: 0 auto; font-size:0.8em; text-align:center ; max-width: 70%;" markdown="1">
Application test using the computed stereo depth to perform visual odometry and point cloud mapping
  </p>
</p>

### Related works
[\[1\] J.-R. Chang and Y.-S. Chen, “Pyramid stereo matching network,” in
CVPR, 2018](https://openaccess.thecvf.com/content_cvpr_2018/papers/Chang_Pyramid_Stereo_Matching_CVPR_2018_paper.pdf)  
[\[2\] F. Zhang, V. Prisacariu, R. Yang, and P. H. Torr, “Ga-net: Guided
aggregation net for end-to-end stereo matching,” in CVPR, 2019.](https://openaccess.thecvf.com/content_CVPR_2019/papers/Zhang_GA-Net_Guided_Aggregation_Net_for_End-To-End_Stereo_Matching_CVPR_2019_paper.pdf)
