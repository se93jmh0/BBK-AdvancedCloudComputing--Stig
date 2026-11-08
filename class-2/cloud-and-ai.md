# How is Artificial Intelligence changing the way cloud infrastructure is designed?

The last few years have seen Cloud Computing at something of an inflection
point.  Traditional data centres typically concentrate on massively scaled CPU
capacity, but—in particular since ChatGPT burst onto the scene—the demand for
GPU compute has rocketed as LLMs find application across a plethora of
knowledge-based disciplines, with no signs of slowing down as more and more
companies embrace the intelligence revolution.

Microsoft's latest play in this market is the Maia 300 architecture, which
evolves the Azure production-live Maia 200 with up to 2.5x more performance
per Watt and up to 7x the token throughput.  This in part is down to Maia's
Software-defined Local Access (SDLA) dataflow architecture, which reimagines
the idea of the tightly integrated RAM caches found on conventional CPUs in
to a more generalized scheme that can be controlled via software.  And thanks
to the vertically-integrated nature of Maia, this flexibility extends outwards
to Ulta Ethernet-based communication: intra-accelerator-pair, intra-pod, and
even intra-superpod.  This approach means that infrastructure can dynamically
scale to workloads with ease, and even route around maintenance and/or hardware
failure, albeit at somewhat reduced performance.

Given the inexorable rise of AI, and the current state of the art, it seems hard
to believe that Microsoft's continuing investment in optimizing for inference
capability in Azure is a misstep.  Commercial compute is experiencing probably
the most significant technology change since its inception, and it feels like
its here to stay.  Maybe in 10 years time the auto accelerating rate of progress 
will make today's data centre hardware look antediluvian.  Based on the way
the industry is going, it could well be that AI itself will be the thing that is
integral to that reality.

Maia 300 Architecture source: https://azure.microsoft.com/en-us/blog/deep-dive-into-azure-maia-300-architecture/