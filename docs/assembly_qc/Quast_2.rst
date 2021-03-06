Assembly evaluation with QUAST(2)
==============================

We run::

  quast.py
  
with the following parameters:

+------------------------------------------+-------------------------+--------------------------------------------------------------------+
| What?                                    | parameter               | Our value                                                          |
+==========================================+=========================+====================================================================+
| The input assembly                       | positional              | ~/workdir/assembly/small_assembly/assembly.contigs.fasta/          |
+------------------------------------------+-------------------------+--------------------------------------------------------------------+ 
| The output directory                     | -o                      | ~/workdir/assembly/small_assembly/quast/                  |
+------------------------------------------+-------------------------+--------------------------------------------------------------------+
| The number of threads to be used         | -t                      | 14                                                                 |
+------------------------------------------+-------------------------+-------------------------------------------numb-------------------------+
| The reference genome used                | -r                      | ~/workdir/wuhan.fasta                                              |
+------------------------------------------+-------------------------+--------------------------------------------------------------------+


The complete commandline is::

  quast.py -t 14 -o ~/workdir/assembly/small_assembly/quast/ -r ~/workdir/wuhan.fasta ~/workdir/assembly/small_assembly/assembly.contigs.fasta 

QUAST generates HTML reports including a number of interactive graphics. To access these reports, open them using a file browser::

  firefox ~/workdir/assembly/small_assembly/quast/report.html
  
Inspect the results - are you satisfied with the assembly?

References
^^^^^^^^^^

**quast** http://sourceforge.net/projects/quast
