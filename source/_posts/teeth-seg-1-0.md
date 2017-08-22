---
title: CBCT分割软件1.0版本小结 | CBCT Segmentation Platform Version 1.0 Notes
date: 2017-08-21 09:07:40
tags: [Image Segmentation, C++, OpenCV, VTK, QT]
---
In the past few months, I was working on designing and developing a Windows desktop software, for teeth segmentation and reconstruction from CBCT images. The system is built with QT. I used VTK for visualization related functions and OpenCV for image processing.

## Workflow
This platform is built as a QT widget application, with `QVTKWidgets` integrated, we could use VTK inside the application.

I use `vtkDicomReader` to read DICOM images from a user defined directory, the data is read as `vtkImageData`. I use `vtkImageViewer2` to render slices. The `vtkImageViewer2` is suitable for display 3d image by slice, by setting view orientation and slice ID, we can have a good view of CBCT data.

Since the initial data is of 3 dimensions, I slice it into a series of 2D images for easy processing afterwards.

I use `vtkContourWidget` to let users select region of interests (ROI) on an initial slice, ROI means the rough bounding box of a tooth. Initial slice are those slices with clear boundary of each tooth.

After picking up an ROI, segmentation procedures are started. The contour will shrink from ROI, the initial contour, iterate and iterate towards the boundary of a tooth. When no or very small changes between two iterations are detected, the iteration is stopped. The last iterate contour is considered to be the segmentation results, or to say the boundary of a specific tooth.

When boundary of a tooth in slice N is found, I push this `vtkContourWidget` into a vector, and convert it into a binary image and save it with ID to a specific directory. And this contour is enlarged for 1 or 2 pixel by some kind of `dialte` algorithm, and then used as the initial contour of next slice, next could be either upper or lower, then the segmentation procedures are looped.

After segmentations of all slices are done, I read all the binary images from workspace with id ordering to form a 3D image data, and use `vtkImageMarchingCubes` to reconstruct 3D model of it. The STL model is exported with `vtkSTLWriter`.

## Segmentation Algorithm

## Acceleration

## Future Improvements
