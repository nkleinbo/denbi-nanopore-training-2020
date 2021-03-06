Get and inspect the WGS dataset
===============================

Get the data
------------

The dataset we are going to use is a whole genome shotgun project from an outbreak in Hongkong.

The dataset is located in our object store. Download it with wget::

  cd ~/workdir
  mkdir data_wgs
  cd data_wgs
  wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/coursedata2020/Cov2_HK_WGS_small.fastq.gz


Remove adapters
---------------

Run porechop on the dataset (try to get the command right on your own)::

  porechop -t 14 -v 2 -i ~/workdir/data_wgs/Cov2_HK_WGS_small.fastq.gz -o ~/workdir/data_wgs/Cov2_HK_WGS_small_porechopped.fastq.gz | tee ~/workdir/data_wgs/porechop.log
  
We save the output with ``tee`` in ``porechop.log`` if you want to reinspect it.


Map the data and inspect with GenomeView
----------------------------------------

Map the data to the Wuhan reference::

  minimap2 -a -t 14 ~/workdir/wuhan.fasta ~/workdir/data_wgs/Cov2_HK_WGS_small_porechopped.fastq.gz | samtools view -b - | samtools sort - > ~/workdir/mappings/Cov2_HK_WGS_small_porechopped_vs_wuhan.sorted.bam
  
We also map the small dataset to the Wuhan reference since we haven't done that yet::

  minimap2 -t 14 -x map-ont -a  ~/workdir/wuhan.fasta ~/workdir/data_artic/basecall_small_porechopped.fastq.gz | samtools view -b - | samtools sort - > ~/workdir/mappings/basecall_small_porechopped_vs_wuhan.sorted.bam

Create the indizes::

  samtools index ~/workdir/mappings/Cov2_HK_WGS_small_porechopped_vs_wuhan.sorted.bam
  samtools index ~/workdir/mappings/basecall_small_porechopped_vs_wuhan.sorted.bam


Load GenomeView with::

  java -jar ~/genomeview-N42.jar
  
Load the Wuhan reference and the mappings and look at the data - is it more equally distributed?


In the next step, we perform the assembly with canu and the WGS dataset.

References
^^^^^^^^^^

**Porechop** https://github.com/rrwick/Porechop

**Minimap2** https://github.com/lh3/minimap2

**samtools** http://www.htslib.org  

**GenomeView** https://genomeview.org/



