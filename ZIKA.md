# ZIKA Pipeline Notes

## Update

* Update citation fields
  * `python vdb/zika_update.py -db vdb -v zika --update_citations`
  * updates `authors`, `title` and `url` fields from genbank files
  * If you get `ERROR: Couldn't connect with entrez, please run again` just run command again
* Update location fields
  * After hand editing `location` in [chateau](https://github.com/blab/chateau)
  * `python vdb/zika_update.py -db vdb -v zika --update_locations`
  * Updates `division`, `country`, `region`, `latitude`, `longitude` fields

## Download

    python vdb/zika_download.py -db vdb -v zika --fstem zika --resolve_method choose_genbank

## Upload

### [ViPR sequences](https://www.viprbrc.org/brc/vipr_genome_search.spg?method=ShowCleanSearch&decorator=flavi_zika)

1. Download sequences
  * Select year >= 2013 and genome length >= 5000
  * Download as Genome Fasta
  * Set Custom Format Fields to 0: GenBank Accession, 1: Strain Name, 2: Segment, 3: Date, 4: Host, 5: Country, 6: Subtype, 7: Virus Species
2. Move downloaded sequences to `fauna/data`
3. Upload to vdb database
  * `python vdb/zika_upload.py -db vdb -v zika --source genbank --locus genome --fname GenomeFastaResults.fasta`

### [Fred Hutch sequences](https://github.com/blab/zika-usvi/tree/master/data)

Upload with:

    python vdb/zibra_upload.py -db vdb -v zika --source fh --locus genome --authors "Black et al" --fname ZIKA_USVI_good.fasta --url https://github.com/blab/zika-usvi/ --title "Genetic characterization of the Zika virus epidemic in the US Virgin Islands"
    python vdb/zibra_upload.py -db vdb -v zika --source fh --locus genome --authors "Black et al" --fname ZIKA_USVI_partial.fasta --url https://github.com/blab/zika-usvi/ --title "Genetic characterization of the Zika virus epidemic in the US Virgin Islands"
