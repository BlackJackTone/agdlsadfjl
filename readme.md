

Thank all reviewers for the constructive reviews. We will address all reviews in the revised paper. 

<br />  
    

### **Common**

C1: Narrative

We will reduce the length of the preliminaries and implementation details, and place more emphasis on novelty in sampling and algorithm selection. The thread will be presented in the following way: 1) We design theoretically feasible sampling solutions, but their performance is unknown. 2) Accordingly, we integrate sampling to 8 multicore join algorithms, and their behaviors demonstrate the huge impact of the actual implementation on all aspects of performance and quality. 3) In turn, we design a decision tree to choose the suitable solution taking both stream and sampling features into consideration.
 
 
C2: Baseline

When we evaluate the method selected by the decision tree, the baseline is the optimal method of the 8 methods mentioned in Sec 2.1. When we evaluate a method in the solution space(i.e. the 14 algorithms), the baseline is the original join algorithm. For example, the baseline of S-MPass is MPass. We will add these details in Sec 6.
 
 
C3: Decision tree

The decision tree in Sec 5.3 has been proven sucessful for real-world datasets, and it can easily be changed to an automatically built structure by adding a training set, adapting to diverse workloads and parallel architectures, including future-proof CPUs. Regarding the thresholds for High and Low, we will add the learned results to the appendix. We will update Sec 5.3 and open source to contribute to the community.
 
 
C4: Hardware

Sec 3.3 shows that the hardware architecture significantly influnces the performance, where the 8-core version with a sampling rate of 0.9 reduces 90%+ lantency compared to the sequential version. For practical use, we develop both thread and data-level parallelisms, and Sec 6.5 demonstrates their scalability.
Besides, as proved in Sec 6.3, sampling and hardware optimizated algorithms need to be studied together because of the influence on both performance and quality. To solve this problem, we develop a decision tree considering both sampling and stream features.
We will detail more in Sec 5.
 
 
<br />

### **Reviewer#1**

O1: Novelty

We claim that an efficient sampling-based intra-window join must holistcly optimize sampling, stream joins, and hardware parallelism. To achieve this goal, we define two sampling functions for each of the stream, one for building and one for probing, which allows tuples to be used for probing even though they are not retained in the sample. Our work fills the blank where there is no sampling designed considering the execution of stream join. To ensure usability, we explored how to design 14 available algorithms and gave a high-speed implementation, and the decision tree is designed to solve selection problems. Moreover, we provide a strong theoretical component associated with the sampling in the appendix, as well as over tens of thousands lines of robust code implementation. We will carefully revise the paper to make our novelty clearer if we are given the precious chance.
 
 
O2: Narrative

See C1.
 
 
O3: Framework

We use framework to refer to the holistc design including sample level, join level, hardware level, and their interaction. We will make it clearer in Sec 4. As to the decision tree in Figure 7, please refer to C3 for our further update.
 
 
<br />

D1: Baseline

See C2.
 
 
D2: Optimality

See C3.
 
 
D3: Hardware

See C4.
 
 
D4: Data utilization

The data utilization of stream R is the fraction of unstored tuples sampled by \sigma' in R. We will make it clearer in Sec 5.1.1.
 
 
D5: Intra-window join

It means joining two input stream over a single window, similar to tumbling window. Specifically, there is no overlap between windows, and leaving out sampling, all the tuples with the same key in the window will be joined. We will add the definition in Sec 1.
 
 
D6: Sketch

It's hard for skech to handle general tasks [14,A]. Its result stream is imaginary and it requires individual designs for different applications, or even different metrics of the same application. Thus they can not fit our requirement of adaptation. We will add more discussion in Sec 7.

\[A\]  Z. Zhao, F. Li, and Y. Liu. "Efficient Join Synopsis Maintenance for Data Warehouse". In SIGMOD 2020.
 
 
D7: Figure 6

We will remove it as suggested.
 

<br />
 
### **Reviewer#2**

O1: Hardware

See C4.
 
 
O2: Writing

See C1.
 
 
O3: Throughput

Sorry for the misunderstanding. Throughput is defined as the number of input tuples processed per unit time, as stated in Sec 3.2. Therefore, the join size output does not contribute to the throughtput. Figure 11 (b) provides an experimental proof of it. Furthermore, the reason for using this definintion is that the definition of latency in this work concerns more about the join output, and we want to show more perspectives of the performance. We will make it clearer in Sec 6.3.
 

<br />
 
### **Reviewer#4**

O1: Adaptation

The adaptation of our work is reflected in that ASSMJoin can satisfy different situations. The required results can be stream data or statistic values, and ASSMJoin can provide various results by adjusting the sampling with techniques detailed in Sec 5.1. The adaptation happens in canceling data materialization and changing sampling methods. We will add these details in Sec 5.1.
 
 
O2: Decision tree

See C3.
 
 
O3: Tradeoff

The tradeoff is reflected in the selection of the appropriate algorithm and sampling rate according to the user's needs. The algorithm selection is settled by the decision tree. The sampling rate is chosen as large as possible under the constraints. For example, in Figure 12 (a), we show the relations between latency and join size. If user limits the latency, the choice is the option with the highest join size under such restriction, which means the tradeoff satisfiying the performance metrics while achieving the suitable quality that can be achieved. We will explain it more clearly in Sec 6.3.
 
 
O4: Figure 7

Sorry for this editorial error. The box Key Duplication(dup) should go out with a Low option, and point to the bottom right box Key Skewness(skew_key). Regarding the scaling to multiple cores, most algorithms perform well, except that MWay scales poorly with increasing input size due to its multi-way merge. We will update Figure 7 and add more details in Sec 5.3.
 
 
O5: Baseline

See C2.
 
 
<br />
 
M1: Key Skewness

Thank you for the careful examination. We will correct that to "uniform".
 
 
M2: The Wording of "..X speedup in throughput"

The ratio of the throughput of our method over that of the baseline.
 

<br />
 
### **Reviewer#5**

O1: Assumption

The assumption can be removed by introducing the order as a property (consistent with the real arrival order) and it does not cause additional memory cost compared to the current variance calculation (if needed). We will show the analysis without assumption and present the results under the current assumption as a special case in Sec 5.1.
 
 
O2: Reservoir sampling

The pseudocode is consistent with both our formula derivation and code implementation. Using "observed stream" for estimation is not an easy problem, and this is one of the reasons why we introduced the order assumption in the O1. If we start join after the reservoir sampling is completely finished, the extra memory used during processing will not bring benefits in result. We will add a detailed discussion of it in Sec 5.1 and present the result not using "observed stream".
 
 
O3: Hardware optimization

See C4.
 
 
O4: 14 algorithms

We will merge the algorithms that have similar behaviors in Figures 10-13 with detailed analysis to make the figures concise.
 
 
<br />
 
T1: Thank you for the correction, and we will remove the redundant references.
 
 
T2: We will move it as suggested.
 
 
T3: We will add more appropriate references to support the argument.
 
 
T4: We will explain more about its usability benefits.
 
 
T5: We apologize for the incorrect example of heuristic sampling, and we will replace the original reference with the appropriate ones, specifically: 

\[A\] T. Johnson, S. Muthukrishnan, I. Rozenbaum. "Sampling algorithms in a stream operator". In SIGMOD 2005.

\[B\] D. L. Quoc, R. Chen, P. Bhatotia, et al. "Streamapprox: Approximate computing for stream analytics". In CoRR 2017.

 
T6: We will explain more the advantages of reservoir sampling and improve the implementation.
 
 
T7: We will clarify the meaning ahead.
 
 
T8: As discribed in Algorithm 1, the hybrid sampling is divided into two independent layers, which are universal and Bernouli sampling with parameters p and q. We will add explanation in Sec 5.1.1.
 
 
T9: We will make it clear ahead in Sec 5.1.
 
 
T10: We percive that the maximum data utilization case just results in a more concise and no simpler case than the minimum data utilization, which not only serves the application but also forms an upper and lower bound together with the minimum utilization case.
 
 
T11: We will detail more in Sec 5.1.
 
 
T12: We will make it clear in Sec 5.2.
 
 
T13: For JM, each kernel is assigned a whole stream R and one of the disjoint subsets of stream S, so the sum of the expectation in each core is consistent with the original version. We will explain it more in Sec 5.3.
 
 
T14: We concluded the phenomenon based on the experimental results, so we will move it to Sec 6. We will try to understand this mathematically and add more discussion.
 
 
Missing references: We will add the missing references.
