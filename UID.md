# Searching for _UID

_UID (Unique ID) is filtered out from global search (v. 1..7.9)

Several fields are filtered out by hardcoding in **Search all individuals**, **Search family records** and **Search the sources* in `FunctionsDb.php`
I'm *not* a fan of hardcoding, so to these functions:
- `searchIndividuals(array $query, array $trees)` 
- `function searchFamilies(array $query, array $trees)`
- `function searchSources($query, $trees)`
- `function searchNotes(array $query, array $trees)`
- `function searchRepositories(array $query, array $trees)`
I had to add content from the configuration 
```
		global $WT_TREE;
		$IgnoreNonGenealogyData = $WT_TREE->getPreference('IGNORE_NON_GENEALOGY_DATA');

			//2017-06-22/EBP: Remove filter for _UID in global search
			//$gedrec = preg_replace('/\n\d (_UID|_WT_USER|FILE|FORM|TYPE|CHAN|RESN) .*/', '', $record->getGedcom());
			$gedrec = preg_replace('/\n\d ('.$IgnoreNonGenealogyData.') .*/', '', $record->getGedcom());
```

And expanded `function findRin($rin)` with:

```
//2017-06-22/EBP Extend findRin() to look for _UID and REFN as well >>>
		if (!$xref) { // Only if XREF not found
			$tag =  20 < (strlen($rin)) ? "_UID" : "REFN" ; // < 20: REFN, > 20: _UID
				$xref = Database::prepare("SELECT i_id FROM `##individuals` WHERE i_gedcom LIKE  CONCAT('% ', ?,' ', ?, '%') AND i_file=?")
				->execute(array($tag, $rin, $WT_TREE->getTreeId()))
				->fetchOne();
		}
//EBP <<<
```
