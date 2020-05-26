The Domain Theory (for recognizing promoters):

   % Promoters have a region where a protein (RNA polymerase) must make contact
   % and the helical DNA sequence must have a valid conformation so that
   % the two pieces of the contact region spatially align.
   % Prolog notation is used.
    promoter :- contact, conformation.

   % There are two regions "upstream" from the beginning of the gene
   % at which the RNA polymerase makes contact.
    contact  :- minus_35, minus_10.

   % The following rules describe the compositions of possible contact regions.
   minus_35 :- p-37=c, p-36=t, p-35=t, p-34=g, p-33=a, p-32=c.
   minus_35 :-         p-36=t, p-35=t, p-34=g,         p-32=c, p-31=a.
   minus_35 :-         p-36=t, p-35=t, p-34=g, p-33=a, p-32=c, p-31=a.
   minus_35 :-         p-36=t, p-35=t, p-34=g, p-33=a, p-32=c.

   minus_10 :- p-14 t, p-13 a, p-12=t, p-11=a, p-10=a, p-9=t. 
   minus_10 :-         p-13 t, p-12=a,         p-10=a,        p-8=t.
   minus_10 :-         p-13 t, p-12=a, p-11=t, p-10=a, p-9=a, p-8=t.
   minus_10 :-                 p-12=t, p-11=a,                       p-7=t.

   % The following rules describe sequence characteristics that produce
   % acceptable conformations.
   conformation :- p-47=c, p-46=a, p-45=a, p-43=t, p-42=t, p-40=a, p-39=c,
                   p-22=g, p-18=t, p-16=c, p-8=g,  p-7=c,  p-6=g,  p-5=c,
                   p-4=c,  p-2=c,  p-1=c. 
   conformation :- p-45=a, p-44=a, p-41=a.
   conformation :- p-49=a, p-44=t, p-27=t, p-22=a, p-18=t, p-16=t, p-15=g, 
                   p-1=a. 
   conformation :- p-45=a, p-41=a, p-28=t, p-27=t, p-23=t, p-21=a, p-20=a,
	           p-17=t, p-15=t, p-4=t.

   % If exact matches are required, this domain theory matches NONE
   % of the examples below.  Also note that some of the MINUS_35 rules
   % are subsumed by another MINUS_35 rule.  This occurs because the
   % biological evidence is inconclusive wrt the correct specificity.

1. Title of Database: E. coli promoter gene sequences (DNA)
                      with associated imperfect domain theory

2. Sources:
   (a) Creators: 
       - promoter instances: C. Harley (CHARLEY@McMaster.CA) and R. Reynolds 
       - non-promoter instances and domain theory: M. Noordewier
         -- (non-promoters derived from work of lab of Prof. Tom Record, 
             University of Wisconsin Biochemistry Department)
   (b) Donor: M. Noordewier and J. Shavlik, {noordewi,shavlik}@cs.wisc.edu
   (c) Date received: 6/30/90

3. Past Usage:
   (a) biological: 
       -- Harley, C. and Reynolds, R. 1987.  
          "Analysis of E. Coli Promoter Sequences."
          Nucleic Acids Research, 15:2343-2361.
       machine learning:
       -- Towell, G., Shavlik, J. and Noordewier, M. 1990.
          "Refinement of Approximate Domain Theories by Knowledge-Based
          Artificial Neural Networks." In Proceedings of the Eighth National
          Conference on Artificial Intelligence (AAAI-90).
   (b) attributes predicted: member/non-member of class of sequences with
       biological promoter activity (promoters initiate the process of gene
       expression).
   (c) Results of study indicated that machine learning techniques (neural
       networks, nearest neighbor, contributors' KBANN system) performed as
       well/better than classification based on canonical pattern matching
       (method used in biological literature).

4. Relevant Information Paragraph:
   This dataset has been developed to help evaluate a "hybrid" learning
   algorithm ("KBANN") that uses examples to inductively refine preexisting
   knowledge.  Using a "leave-one-out" methodology, the following errors
   were produced by various ML algorithms.  (See Towell, Shavlik, &
   Noordewier, 1990, for details.)

	    System	 Errors		Comments
	    ------	 ------		--------
	     KBANN	  4/106		a hybrid ML system
	     BP		  8/106		std backprop with one hidden layer
	     O'Neill	 12/106		ad hoc technique from the bio. lit.
	     Near-Neigh  13/106		a nearest-neighbor algo (k=3)
	     ID3	 19/106		Quinlan's decision-tree builder
	     	
   Type of domain: non-numeric, nominal (one of A, G, T, C)
   -- Note: DNA nucleotides can be grouped into a hierarchy, as shown below:

		      X (any)
		    /   \
	  (purine) R     Y (pyrimidine)
		  / \   / \
		 A   G T   C

 
5. Number of Instances: 106

6. Number of Attributes: 59
   -- class (positive or negative)
   -- instance name
   -- 57 sequential nucleotide ("base-pair") positions

7. Attribute information:
   -- Statistics for numeric domains: No numeric features used.
   -- Statistics for non-numeric domains
      -- Frequencies:  Promoters Non-Promoters
                       --------- -------------
               A        27.7%     24.4%
               G        20.0%     25.4%
               T        30.2%     26.5%
               C        22.1%     23.7%

   Attribute #:  Description:
   ============  ============
             1   One of {+/-}, indicating the class ("+" = promoter).
             2   The instance name (non-promoters named by position in the
                 1500-long nucleotide sequence provided by T. Record).
          3-59   The remaining 57 fields are the sequence, starting at 
                 position -50 (p-50) and ending at position +7 (p7). Each of
                 these fields is filled by one of {a, g, t, c}.

8. Missing Attribut


