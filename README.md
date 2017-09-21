<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd"><HTML><!-- v:10.0.7.13 --><HEAD 
<META content="IE=9.0000" http-equiv="X-UA-Compatible">
<DIV id="contentArea">
<DIV class="zone" id="mainZone">
<DIV class="compositeModule_1Zone ">
<DIV class="zone">
<DIV class="title deM"><B><H2>Employing Semantic Context for Sparse Information Extraction Assessment</H2></B>
<DIV class="cl"></DIV></DIV>
<DIV class="conM ">
<P>&nbsp;</P>
<P>We address two problems in this paper. We first want to veri- fy the
correctness of hundreds of millions of isA relationships. That is,
given a candidate pair &lt;c,e&gt;, we want to evaluate how
likely e is an entity of class c. Second, given a candidate pair
&lt;e1, e2&gt;, and a known relationship R between classes c1 and
c2, we want to evaluate whether relationship R exists between
e1 and e2.</P>
<H2>Introduction</H2>
<P>The explosive growth and popularity of the World Wide
Web has resulted in a huge amount of texts on the
Internet, which presents an unprecedented opportunity for Information Extraction (IE).
IE is at the core of many emerging applications,
such as entity search, text mining, 
and risk analysis using financial reports.
In these applications, we can divide the outcome of IE into two categories according to the frequency: heads and tails. The heads are those that occur very
frequently in the corpus. For instance, we can extract the fact that "google is a company" from numerous distinct
sentences. It is built on the assumption that the higher the frequency, the more likely
it is correct. Nevertheless, there are results that occur very
infrequently, for instance, suppose from a corpus we extract a
statement that says Rhodesia(Rhodesia was an
    unrecognised state located in southern Africa that existed between
    1965 and 1979 following its Unilateral Declaration of Independence
    from the United Kingdom on 11 November 1965.) is a country, and
its occurrences in the corpus are few and far between. In
Table 1, we show some frequent and rare candidate
countries extracted from a web corpus using Hearst
patterns. It turns out that all frequent entities are correct, while
the majority of infrequent ones are incorrect. The mistakes come from 
either the extraction algorithm, or erroneous sentences in
the corpus.</P>
<P align="left"><B>Table 1: Frequent and infrequent candidate entities of country</B></P>
<table align="center">
  <TR>
    <TD align="center"><B>Frequent Entities</B></TD>
    <TD align="center"><B>Rare Entities</B></TD>
</TR>
  <TR>
    <TD align="center">India</TD>
    <TD align="center">Northern</TD>
</TR>
  <TR>
    <TD align="center">China</TD>
    <TD align="center">Sabah</TD>
</TR>
  <TR>
    <TD align="center">Germany</TD>
    <TD align="center">Yap</TD>
</TR>
  <TR>
    <TD align="center">Australia</TD>
    <TD align="center">Parts of sudan</TD>
</TR>
  <TR>
    <TD align="center">Japan</TD>
    <TD align="center">Wealthy</TD>
</TR>
  <TR>
    <TD align="center">France</TD>
    <TD align="center">Western romania</TD>
</TR>
  <TR>
    <TD align="center">Canada</TD>
    <TD align="center">American artists</TD>
</TR>
  <TR>
    <TD align="center">USA</TD>
    <TD align="center">South korea japan</TD>
</TR>
  <TR>
    <TD align="center">Brazil</TD>
    <TD align="center">New sjaelland</TD>
</TR>
  <TR>
    <TD align="center">Italy</TD>
    <TD align="center">Rhodesia</TD>
</TR>
</table>

<P>How to verify the correctness of a tail extraction
(also known as sparse extraction) is one of the most
important and challenging problems in IE. As we know,
the distribution of words and phrases in a corpus of
natural language utterances follows the Zipf's law which states that the frequency of any word or phrase is
inversely proportional to its rank in the frequency table.
Thus, their occurrences in a particular syntactic pattern
we use for extraction are very small. Without a good
mechanism to identify correct extractions from incorrect
ones, sparse information extraction will be plagued by
either low precision or low recall.</P>
<P>Existing efforts in information extraction or sparse extraction
can be divided into the following four classes. Heuristic based approaches start with a set of seed
entities given a relation or some prior label distributional
knowledge, and identify extraction patterns for
the relation iteratively. Redundancy-based approaches require that extractions
appear relatively frequently with a limited set of patterns. Knowledge-based approaches identify information extraction
in terms of external resources, such as Wikipedia, Freebase and WordNet. In addition, most of popular approaches in handling
of sparse extractions are context-based model building
approaches. They use one important hypothesis known
as the distributional hypothesis, which says that different
entities of the same semantic relation (such as the
unary and binary relations) tend to appear in similar
textual contexts. For example, we may not find many
occurrences of Rhodesia in the Hearst pattern "countries
such as Rhodesia". But if Rhodesia appears in similar
context where terms such as India, USA, and Germany
occur, then we will be more certain about the claim
that Rhodesia is a country according to the distributional
hypothesis. This hypothesis is beneficial to assess sparse
extractions.However, the challenge lies in modeling contexts and
measuring the semantic similarity of two contexts.</P>
<H2>Our Semantic Context based Approach for Assessing Sparse Information Extractions</H2>
<P>We now analyze the challenges in the tasks. The first
challenge is the scale. For example, there are hundreds of
millions of isA relationships (formed among 2.7 million
categories and 5.5 million entities in Probase[1][2]). It is
impossible to learn the generative model (such as the
HMM model and the deep learning model) based on
the contexts of all entities, it is very time-consuming. The
second challenge lies in improving the effectiveness of
the verifier. As we mentioned, the feature representation
based on the contexts of words are very different that
based on the contexts of entities. Meanwhile, neither a
bag of words nor a set of hidden states can provide
good semantics to understand the relationship between
a candidate pair.
Motivated by this, in this paper, we introduce a
semantic, scalable, and effective approach for sparse
information extraction assessment.  
<P><H3>The main contributions of this paper are as follows.</H3></P>
<P>First, we introduce a semantic approach for solving the two problems. More precisely, we
come up with a semantic representation of the contexts. This approach is natural because we
are dealing with a large semantic network, which provides semantic information in various
aspects. Using these information, we are able to introduce semantic features to describe a
context, which leads to a lightweight and effective solution of context learning.</P>
<P>Second, we scan billions of web documents using MapReduce6 to capture the contexts of
millions of entities and pairs of entities in Probase, and then compare the similarity between
their contexts and the contexts of seeds7. We further use the similarity evaluated by our
three semantic context based approaches to represent the feature space given a pair, and
then train a binary-class classifier on a small number of labeled data varying with different
base classifiers to select the best one for predicting sparse extractions. Extensive studies 
show that our approach can achieve better performance than state-of-the-art approaches in
sparse extraction assessment.</P>
<H2>Data Set </H2>
<P>Considering the experimental data sets, we randomly
selected about 1800 entities that belong to 12 classes in
Probase. Tables 2 and 3 show the descriptions and some
examples in each class respectively. Each entity has no
more than 10 occurrences in Hearst patterns and we call
them sparse extractions. This is because more than 90%
entities of the above 12 concepts have no more than 10
occurrences in Probase, namely lying in the long tail
of the entity distribution curves. For example, Figure
2 shows the frequency distribution varying the number
of entities in country. We can clearly see the long tail
phenomenon under the dotted line with no more than
10 occurrences. We asked human judges to evaluate their
correctness.We also looked into three binary relations: is-
CapitalOf, isCurrencyOf, and headquarteredIn. We randomly
picked 315 sparse extractions that have no more than
10 occurrences, and we also picked the 10 most frequent
extractions for each relation which serve as seeds. Details of all test relationships are shown in Table 2.</P>
</P>
<P align="center"><B>Table 2: Data sets used in experiments</B></P>
<TABLE align="center" class=" borderColumns borderRows tableBorder" cellSpacing="0" cellPadding="0">
  <TBODY>
  <TR>
    <TD align="center"><B></B></TD>
    <TD align="center"><B>total pairs in Probase</B></TD>
    <TD align="center"><B>paris with frequency < 10 </B></TD>
	<TD align="center"><B>pairs in experiments</B></TD>
    <TD align="center"><B>#bad pairs</B></TD>
    <TD align="center"><B>#good pairs</B></TD>
</TR>
  <TR>
    <TD align="center" colspan="6">isA relationships</TD>
</TR>
  <TR>
    <TD align="center"><B>country</B></TD>
    <TD align="center"><B>5534</B></TD>
    <TD align="center"><B>92.81% </B></TD>
	<TD align="center"><B>415</B></TD>
    <TD align="center"><B>226</B></TD>
    <TD align="center"><B>189</B></TD>
</TR>
  <TR>
    <TD align="center"><B>sport</B></TD>
    <TD align="center"><B>2866</B></TD>
    <TD align="center"><B>92.18% </B></TD>
	<TD align="center"><B>335</B></TD>
    <TD align="center"><B>67</B></TD>
    <TD align="center"><B>268</B></TD>
</TR>
  <TR>
    <TD align="center"><B>city</B></TD>
    <TD align="center"><B>8815</B></TD>
    <TD align="center"><B>90.05% </B></TD>
	<TD align="center"><B>231</B></TD>
    <TD align="center"><B>33</B></TD>
    <TD align="center"><B>198</B></TD>
</TR>
  <TR>
    <TD align="center"><B>animal</B></TD>
    <TD align="center"><B>5562</B></TD>
    <TD align="center"><B>92.38% </B></TD>
	<TD align="center"><B>186</B></TD>
    <TD align="center"><B>37</B></TD>
    <TD align="center"><B>149</B></TD>
</TR>
  <TR>
    <TD align="center"><B>seasoning</B></TD>
    <TD align="center"><B>531</B></TD>
    <TD align="center"><B>92.47% </B></TD>
	<TD align="center"><B>169</B></TD>
    <TD align="center"><B>41</B></TD>
    <TD align="center"><B>128</B></TD>
</TR>
  <TR>
    <TD align="center"><B>company</B></TD>
    <TD align="center"><B>59734</B></TD>
    <TD align="center"><B>96.84%</B></TD>
	<TD align="center"><B>82</B></TD>
    <TD align="center"><B>9</B></TD>
    <TD align="center"><B>73</B></TD>
</TR>
  <TR>
    <TD align="center"><B>painter</B></TD>
    <TD align="center"><B>1097</B></TD>
    <TD align="center"><B>98.09% </B></TD>
	<TD align="center"><B>81</B></TD>
    <TD align="center"><B>5</B></TD>
    <TD align="center"><B>76</B></TD>
</TR>
  <TR>
    <TD align="center"><B>currency</B></TD>
    <TD align="center"><B>330</B></TD>
    <TD align="center"><B>91.82%</B></TD>
	<TD align="center"><B>78</B></TD>
    <TD align="center"><B>8</B></TD>
    <TD align="center"><B>70</B></TD>
</TR>
  <TR>
    <TD align="center"><B>disease</B></TD>
    <TD align="center"><B>8280</B></TD>
    <TD align="center"><B>92.60%</B></TD>
	<TD align="center"><B>69</B></TD>
    <TD align="center"><B>9</B></TD>
    <TD align="center"><B>60</B></TD>
</TR>
  <TR>
    <TD align="center"><B>film</B></TD>
    <TD align="center"><B>10859</B></TD>
    <TD align="center"><B>96.62%</B></TD>
	<TD align="center"><B>65</B></TD>
    <TD align="center"><B>25</B></TD>
    <TD align="center"><B>40</B></TD>
</TR>
  <TR>
    <TD align="center"><B>language</B></TD>
    <TD align="center"><B>2703</B></TD>
    <TD align="center"><B>93.53% </B></TD>
	<TD align="center"><B>51</B></TD>
    <TD align="center"><B>6</B></TD>
    <TD align="center"><B>45</B></TD>
</TR>
 <TR>
    <TD align="center"><B>river</B></TD>
    <TD align="center"><B>1924</B></TD>
    <TD align="center"><B>97.77%</B></TD>
	<TD align="center"><B>40</B></TD>
    <TD align="center"><B>2</B></TD>
    <TD align="center"><B>38</B></TD>
</TR>
 <TR>
    <TD align="center"><B>total</B></TD>
    <TD align="center"><B>108235</B></TD>
    <TD align="center"><B>92.25%</B></TD>
	<TD align="center"><B>1802</B></TD>
    <TD align="center"><B>468</B></TD>
    <TD align="center"><B>1334</B></TD>
</TR>
<TR>
    <TD align="center" colspan="6">Binary relationships</TD>
</TR>
<TR>
    <TD align="center" colspan="3">isCapitalOf(country, city)</TD>
	<TD align="center"><B>160</B></TD>
    <TD align="center"><B>39</B></TD>
    <TD align="center"><B>121</B></TD>
</TR>
<TR>
    <TD align="center" colspan="3">isCurrencyOf(country, currency)</TD>
	<TD align="center"><B>80</B></TD>
    <TD align="center"><B>19</B></TD>
    <TD align="center"><B>61</B></TD>
</TR>
<TR>
    <TD align="center" colspan="3">headquarteredIn(company, city)</TD>
	<TD align="center"><B>75</B></TD>
    <TD align="center"><B>22</B></TD>
    <TD align="center"><B>235</B></TD>
</TR>
<TR>
    <TD align="center" colspan="3">total</TD>
	<TD align="center"><B>315</B></TD>
    <TD align="center"><B>80</B></TD>
    <TD align="center"><B>235</B></TD>
</TR>
</TBODY></TABLE>

<P align="left"><B>Table 3: Examples of isA relations </B></P>
<P>
<TABLE align="center" class=" borderColumns borderRows tableBorder" cellSpacing="0" cellPadding="0">
  <TR>
    <TD align="center"><B>isA relation</B></TD>
    <TD align="center"><B>#bad pair</B></TD>
    <TD align="center"><B>#good pair</B></TD>
</TR>
  <TR>
    <TD align="center"><B>country</B></TD>
    <TD align="center"><B>&lt;country, democratic people&gt;</B></TD>
    <TD align="center"><B>&lt;country, g77&gt;</B></TD>
</TR>
   <TR>
    <TD align="center"><B>city</B></TD>
    <TD align="center"><B>&lt;city, santa martha&gt;</B></TD>
    <TD align="center"><B>&lt;city, amadora&gt;</B></TD>
</TR>
 <TR>
   <TD align="center"><B>sport</B></TD>
    <TD align="center"><B>&lt;sport, trafalgar park&gt;</B></TD>
    <TD align="center"><B>&lt;sport, girls golf&gt;</B></TD>
</TR>
  <TR>
   <TD align="center"><B>animal</B></TD>
    <TD align="center"><B>&lt;animal, cauquenes&gt;</B></TD>
    <TD align="center"><B>&lt;animal, moon snail&gt;</B></TD>
</TR>
 <TR>
  <TD align="center"><B>seasoning</B></TD>
    <TD align="center"><B>&lt;seasoning, bacon bit&gt;</B></TD>
    <TD align="center"><B>&lt;seasoning, five spice&gt;</B></TD>
</TR>
  <TR>
   <TD align="center"><B>company</B></TD>
    <TD align="center"><B>&lt;company, institute&gt;</B></TD>
    <TD align="center"><B>&lt;company, hasbro&gt;</B></TD>
</TR>
 <TR>
  <TD align="center"><B>painter</B></TD>
    <TD align="center"><B>&lt;painter, robert young&gt;</B></TD>
    <TD align="center"><B>&lt;painter, childe hassam&gt;</B></TD>
</TR>
  <TR>
   <TD align="center"><B>film</B></TD>
    <TD align="center"><B>&lt;film, forest gump&gt;</B></TD>
    <TD align="center"><B>&lt;film, breach&gt;</B></TD>
</TR>
 <TR>
  <TD align="center"><B>language</B></TD>
    <TD align="center"><B>&lt;language, francophone&gt;</B></TD>
    <TD align="center"><B>&lt;language, micmac&gt;</B></TD>
</TR>
  <TR>
   <TD align="center"><B>river</B></TD>
    <TD align="center"><B>&lt;river, manda&gt;</B></TD>
    <TD align="center"><B>&lt;river, missouri river&gt;</B></TD>
</TR>
  <TR>
   <TD align="center"><B>Binary Relation</B></TD>
    <TD align="center"><B>#bad pair</B></TD>
    <TD align="center"><B>#good pair</B></TD>
</TR>
  <TR>
   <TD align="center"><B>isCapitalOf(country, city)</B></TD>
    <TD align="center"><B>&lt;dili, east timor&gt;</B></TD>
    <TD align="center"><B>&lt;andorra, andorra la Vella&gt;</B></TD>
</TR>
<TR>
    <TD align="center"><B>isCurrencyOf(country, currency)</B></TD>
    <TD align="center"><B>&lt;baht, thailand&gt;</B></TD>
    <TD align="center"><B>&lt;colombia, colombian peso&gt;</B></TD>
</TR>
<TR>
    <TD align="center"><B>headquarteredIn(company, city);</B></TD>
    <TD align="center"><B>&lt;espoo, general electric&gt;</B></TD>
    <TD align="center"><B>&lt;michelin, clermont-ferrand&gt;</B></TD>
</TR>
</TABLE>
</P>

<P align="left"><B>Table 2: Overall Performance on 12 isA relationships</B></P>
<P align="center">
<TABLE align="center" class=" borderColumns borderRows tableBorder" cellSpacing="0" cellPadding="0">
  <TR>
    <TD align="center"><B>Method</B></TD>
    <TD align="center"><B>BR</B></TD>
    <TD align="center"><B>BP</B></TD>
    <TD align="center"><B>GR</B></TD>
    <TD align="center"><B>GP</B></TD>
	<TD align="center"><B>BF1</B></TD>
    <TD align="center"><B>GF1</B></TD></TR>
  <TR>
    <TD align="center">BM</TD>
    <TD align="center">14.9</TD>
    <TD align="center">30.3</TD>
    <TD align="center">87.7</TD>
    <TD align="center">74.1</TD>
	<TD align="center">19.9(5)</TD>
	<TD align="center">80.3(6)</TD>
</TR>
<TR>
    <TD align="center">PM</TD>
    <TD align="center">18.0</TD>
    <TD align="center">36.5</TD>
    <TD align="center">88.8</TD>
    <TD align="center">75.2</TD>
	<TD align="center">24.1(4)</TD>
	<TD align="center">81.4(4)</TD>
</TR>
<TR>
    <TD align="center">CM</TD>
    <TD align="center">7.9</TD>
    <TD align="center">24.2</TD>
    <TD align="center">91.9</TD>
    <TD align="center">75.2</TD>
	<TD align="center">11.9(6)</TD>
	<TD align="center">82.7(3)</TD>
</TR>
<TR>
    <TD align="center">AM</TD>
    <TD align="center">41.9</TD>
    <TD align="center">50.3</TD>
    <TD align="center">85.6</TD>
    <TD align="center">81</TD>
	<TD align="center">45.7(3)</TD>
	<TD align="center">83.2(2)</TD>
</TR>
<TR>
    <TD align="center">IM</TD>
    <TD align="center">64.6</TD>
    <TD align="center">49.1</TD>
    <TD align="center">76.5</TD>
    <TD align="center">86.1</TD>
	<TD align="center">55.8(2)</TD>
	<TD align="center">81.0(5)</TD>
</TR>
<TR>
    <TD align="center">AIC</TD>
    <TD align="center">56.7</TD>
    <TD align="center">62.0</TD>
    <TD align="center">88.5</TD>
    <TD align="center">86.0</TD>
	<TD align="center">59.2(1)</TD>
	<TD align="center">87.2(1)</TD>
</TR>
</TABLE>
 </P>
<P></P>
<DIV style="clear: both;"></DIV>
<DIV class="conM ">
<H2>Used Data Sets: Download</H2>
<P>More Details Refer to <A onclick="stc(this, 26)" href="http://121.42.218.45/peipeili/Used-Data-Sets-and-demo.rar" 
target="_new"> Used Data Sets</A>.</P></DIV>
<DIV style="clear: both;"></DIV>
<DIV class="conM ">
<H2>Source codes: Download</H2>
<P>More Details Refer to <A onclick="stc(this, 26)" href="http://121.42.218.45/peipeili/ShortTextClassification-src.rar" 
target="_new"> Source codes</A>.</P></DIV>
<DIV style="clear: both;"></DIV>
<DIV class="conM ">
<H2>References</H2>
<P>[1] Knowledgebase Probase: http://research.microsoft.com/en-us/projects/probase/release.aspx</P>
<P>[2] W. Wu, H. Li, H. Wang, and K. Q. Zhu. Probase: a probabilistic taxonomy 
for text understanding. In Proceedings of SIGMOD'12, pages 481-492, 2012.</P>
</DIV>
<DIV class="conM ">
<H2>Contact</H2>
<P><A title="" style="zoom: 1;" onclick="stc(this, 30)" href="http://ci.hfut.edu.cn/index/teacherinfo/tid/522" 
target="_new" alt="">Peipei Li</A> (peipeili@hfut.edu.cn): Hefei University of Technology, China<BR>
<A title="" style="zoom: 1;" onclick="stc(this, 30)" href="http://haixun.olidu.com/" 
target="_new" alt="">Haixun Wang</A> (haixun@google.com): Google Research, USA <BR><A title="" style="zoom: 1;" onclick="stc(this, 29)" 
target="_new" alt="">Hongsong Li</A> (hongsong.lhs@alibaba-inc.com): Alibaba Group, China <BR><A title="" style="zoom: 1;" onclick="stc(this, 30)" href="http://www.ucs.louisiana.edu/~xxw8007/" 
target="_new" alt="">Xindong Wu</A> (xwu@uvm.edu): University of Louisiana at Lafayett, USA</P>
<P class="smallText"></P>
<P class="smallText">&nbsp;</P></DIV>
<DIV style="clear: both;"></DIV></DIV>
<DIV style="clear: left;"></DIV></DIV></DIV></DIV><!--NOINDEX_START-->					 
<DIV class="cl"></DIV>
<DIV class="bt" id="bGrad"></DIV></DIV></DIV>
		 </DIV>     
 </DIV></BODY></HTML>
