---
title: Input Assembler Stage
description: Input Assembler Stage
ms.assetid: 8db6a2ab-8354-4690-8141-2cdd91c77d5c
---

# Input Assembler Stage


The input assembler (IA) introduces triangles, lines, or points into the rendering pipeline by pulling source geometry data out of 1D buffers.

Vertex data can come from multiple buffers, and can be accessed in an array-of-structures fashion from each buffer. The buffers are each bound to an individual input slot and given a structure stride. The layout of data across all the buffers is specified by an input declaration, in which each entry defines an *element*. The element contains an input slot, a structure offset, a data type, and a target register (for the first active shader in the pipeline).

A given sequence of vertices is constructed out of data that is fetched from buffers. The data is fetched in a traversal that is directed by a combination of fixed-function state and various *Draw\**() DDI calls. Various primitive topologies (for example, point-list, line-list, triangle-list, and triangle-strip) are available to make the sequence of vertex data represent a sequence of primitives.

Vertex data can be produced in one of two ways. The first way to produce vertex data is *non-indexed* rendering, which is the sequential traversal of buffers that contain vertex data. The vertex data originates at a start offset at each buffer binding. The second way to produce vertex data is *indexed* rendering, which is sequential traversal of a single buffer that contains scalar integer indexes. The indexes originate at a start offset into the buffer. Each index indicates where to fetch data out of a buffer that contains vertex data. The index values are independent of the characteristics of the buffers that they refer to. Buffers are described by declarations. Non-indexed and indexed rendering, each in their own way, produce addresses from which to fetch vertex data in memory, and subsequently assemble the results into vertices and primitives.

Instanced geometry rendering is enabled by allowing the sequential traversal, in either non-indexed or indexed rendering, to loop over a range within each vertex buffer (non-indexed case) or index buffer (indexed case). Buffer-bindings can be identified as *instance data* or *vertex data*. This identification specifies how to use the bound buffer while performing instanced rendering. The address that is generated by non-indexed or indexed rendering is used to fetch vertex data, which also accounts for looping when the runtime performs instanced rendering. Instance data, on the other hand, is always sequentially traversed starting from a per-buffer offset, at a frequency equal to one step per instance (for example, one step forward after the number of vertices in an instance are traversed). The step rate for instance data can also be chosen to be a sub-harmonic of the instance frequency (that is, one step forward every other instance, every third instance, and so on).

Another special case of the IA is that it can read buffers that the stream output stage wrote to. Such a scenario enables a new type of draw operation, [**DrawAuto**](https://msdn.microsoft.com/library/windows/hardware/ff556123). *DrawAuto* allows a dynamic amount of output that was written to stream-output buffers to be reused, without the CPU involvement, to determine how much data was actually written.

In addition to producing vertex data from buffers, the IA can auto-generate three scalar counter values: VertexID, PrimitiveID, and InstanceID, for input to shader stages in the rendering pipeline.

In indexed rendering of strip topologies, such as triangle strips, a mechanism is provided for drawing multiple strips with a single *Draw\**() call (that is, the **cut** command to cut strips).

The Direct3D runtime calls the following driver functions to create, set up, and destroy the IA:

[**CalcPrivateElementLayoutSize**](https://msdn.microsoft.com/library/windows/hardware/ff538289)

[**CreateElementLayout**](https://msdn.microsoft.com/library/windows/hardware/ff540640)

[**DestroyElementLayout**](https://msdn.microsoft.com/library/windows/hardware/ff552771)

[**IaSetIndexBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff567387)

[**IaSetInputLayout**](https://msdn.microsoft.com/library/windows/hardware/ff567389)

[**IaSetTopology**](https://msdn.microsoft.com/library/windows/hardware/ff567390)

[**IaSetVertexBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff567392)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20Input%20Assembler%20Stage%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



