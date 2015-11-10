[![DOI](https://zenodo.org/badge/18586/DataSciBurgoon/aopxiv.svg)](https://zenodo.org/badge/latestdoi/18586/DataSciBurgoon/aopxiv)

# README for input\_data\_format.json and input\_data\_format_omics.json
The input files are in the JSON format. All entries under "bioassay" require values from the Bioassay Ontology (BAO).
Examples are included in this file, and example files are also included in this directory.

# input\_data\_format.json

## Sections
The input file has two main sections. The first one, Submitter, captures information about the submitter. The second section,
Bioassay, captures information about the assay and its data. The Bioassay section utilizes the Bioassay Ontology.


### Submitter
 - firstName: This is your first name
 - lastName: This is your last name
 - email: This is your email

### Bioassay
 - assayName [required]: The name of the assay
 - assayManufacturer [required]: The name of the assay manufacturer. If this is an in-house assay, then give the name
    of the PI/Laboratory Director, and the institution's name, such as: "Hubert Farnsworth, Mars University"
 - type [required]: This is a type or subclass of bioassay. For instance, "oxidoreductase activity assay" is a type of bioassay. Bioassay
    can be found under "assay bioassay component". To be specific, "oxidoreductase activity assay" is a type of "enzyme activity assay"
    which is a type of "bioassay."
 - species [required]: The latin Genus species of the species of the assay. If the assay is a cellular assay, then the
    Genus species should reflect that of the cell being used.
 - origin [required]: The tissue or organ of origin -- be as specific as practical. If you can specify a tissue, then please do so.
 - cellLineName [required]: If you are using a cell line with a recognized name or identifier please use it. For instance,
    if you're using a GripTite 293 MSR cell line, you'd state that. If you're using a HEK cell ine, state that.
 - cellType [required]: One of these: primary cell, immortalized cell, cancer-derived cell
 - measuredEntity [required]: This is a molecular entity in the Bioassay Ontology. A measured entity is the thing that an assay is actually measuring.
    For instance, an assay may actually be measuring "tumor necrosis factor alpha" protein levels. Or, an assay may actually be measuring a
    specific proteolytic cleavage product, such as "angiotensinogen proteolytic cleavage product". If your particular measured entity does not
    exist within the Bioassay Ontology then enter it here, and place two $$ after the name, such as: ethylmethylbadstuff$$
    Note: You may need to specify a biological macromolecule here, such as Beta-lactamase, and that's okay for our purposes.
 - measuredEntitySpecies [required]: The Genus species of the measured entity.
 - targetMacromolecule [required/optional]: You must either have a targetMacromolecule, or a target, but not both.
    This is a biological macromolecule in the Bioassay Ontology. This is also known as the "intended target."
    We are aware that in some cases the intended target is actually not a macromolecule (e.g., cell viability based on cell number/counts).
    In these cases target is required.
    Note: You may need to specify your own entry here. For instance, none of the ligand-activated nuclear receptors or ligand-activated
    transcription factors are listed in this part of the BAO. This is another field that we will be extending in the future with the
    AOPO.
 - targetMacromoleculeSpecies [required/optional]: The Genus species of the target macromolecule. Only required when the targetMacromolecule is required.
    If you don't know, type unknown.
 - target [required/optional]: You must either have a targetMacromolecule, or a target, but not both. Currently, there is
    no ontology for these terms. AOP Ontology staff will standardize these terms in the future. For now, enter a reasonable
    target, such as cell number, or something that has an obvious meaning. Once standardized terms are released, we will
    update this description.
 - targetSpecies [required/optional]: Genus species of the target. Only required when the target is required.
 - bioassaySpecification [required]: This is a comma separated list of bioassay specifications from the Bioassay Ontology. Bioassay specifications are found under assay bioassay component in the Bioassay Ontology. Here's an example:
    1536 well plate, multiple concentration, endpoint assay, image-based readout
 - physicalDetectionMethod [required]: This is a physical detection method from the Bioassay Ontology. Physical
    detection methods are under assay method component in the Bioassay Ontology.
 - assayDesignMethod [required]: This is the assay design method from the Bioassay Ontology. Assay design methods
    can be found under assay method which is under assay method component in the Bioassay Ontology.
 - assayFormat [required]: This is the assay format in the Bioassay Ontology. These can be found under assay format component
    in the Bioassay Ontology.
 - pubchemAID [optional]: This is the assay identification number from PubChem. This is optional, but helpful if it exists
    for cross-referencing.
 - measureGroup [required]: This contains the data. If you don't want to include the data in-line (i.e., in the file
    there is another file format that allows you to keep the raw data in a tab-delimited text file, and specify the name of the
    file here. If that's how you want to upload your data, please see the input\_data\_format\_external.json or
    input\_data\_format\_omics\_external.json files).


# input\_data\_format.json example
```
{
	"submitter": {
		"firstName": "Lyle",
		"lastName": "Burgoon",
		"email": "Lyle.D.Burgoon@usace.army.mil"
	},
	"bioassay": {
	    "assayName": "BG1-Luc-4E2",
	    "assayManufacturer": "University of California",
		"type": "luciferase enzyme activity assay",
		"species": "Homo sapiens",
		"origin": "ovarian neoplasm",
		"cellLineName": "BG-1",
		"cellType": "immortalized",
		"measuredEntity": "luciferin",
		"measuredEntitySpecies": "unknown",
		"targetMacromolecule": "Estrogen receptor alpha",
		"targetMacromoleculeSpecies": "Homo sapiens",
		"bioassaySpecification": "1536 well plate, multiple concentration, endpoint assay, imaged-based readout, single readout",
		"physicalDetectionMethod": "fluorescence resonance energy transfer",
		"assayDesignMethod": "luciferase induction",
		"assayFormat": "cell based format",
		"pubchemAID": "AID 743080",
		"measureGroup": [
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.00123"}, "value": "3.2246"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.00275"}, "value": "9.0507"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.00614"}, "value": "-4.4693"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.014"}, "value": "0.1532"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.031"}, "value": "-6.8577"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.068"}, "value": "-7.2284"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.153"}, "value": "-18.4067"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.341"}, "value": "-18.4813"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "0.762"}, "value": "-20.3226"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "1.703"}, "value": "-30.668"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "3.794"}, "value": "-31.2702"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "8.468"}, "value": "-30.5666"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "18.17"}, "value": "-44.2772"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "32.48"}, "value": "-41.7873"} },
			{"screenedEntity": "Benzo[k]fluoranthene", "endpoint": {"type": "percent response", "screeningConcentration": {"has_concentration_unit": "micromolar", "has_concentration_value": "70.35"}, "value": "-38.1683"} }
		]
	}
}
```
