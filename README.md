[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4569929.svg)](https://doi.org/10.5281/zenodo.4569929)

# Corpus of Czech Verse

This repo contains 1305 out of 1689 books of poetry from the [Corpus of Czech Verse](http://versologie.cz/v2/web_content/corpus.php?lang=en) (384 books are still covered by copyright protection).

JSON files comprise not only the text themselves and their metadata but also:
<ul>
	<li>thourough annotation of poetic meters</li>
	<li>annotation of rhymes</li>
	<li>phonetic transcription</li>
	<li>tokenization</li>
	<li>lemmatization</li>
	<li>morphological tagging</li>
</ul>

*NOTE: There are several re-editions in the corpus. One poem thus may appear multiple times.

## Structure

Each file holds poems comming from a single book of poetry. Each poem is a dict with following structure:

```python
{
	'book_id': ID OF THE BOOK,
	'poem_ids': ID OF THE POEM,

	# Metadata on author or the editor of the entire book
	'b_author': {
		'identity': REAL NAME OF THE AUTHOR,
		'name': NAME AS PRINTED IN THE BOOK #it differs from 'identity' in case of pen name,
		'born': THE YEAR AUTHOR WAS BORN,
		'died': THE YEAR AUTHOR DIED,
	},

	# Metadata on author of the poem
	'p_author': {
		'identity': REAL NAME OF THE AUTHOR,
		'name': NAME AS PRINTED IN THE BOOK #it differs from 'identity' in case of pen name,
		'born': THE YEAR AUTHOR WAS BORN,
		'died': THE YEAR AUTHOR DIED,
	},
	
	'biblio': {
		'p_title': TITLE OF THE POEM,
		'b_title': TITLE OF THE BOOK,
		'b_subtitle': SUBTITLE OF THE BOOK,
		'publisher': PUBLISHER OF THE BOOK,
		'place': PLACE WHERE PUBLISHED,
		'year': YEAR WHEN PUBLISHED,
		'pages': PAGE RANGE OF THE POEM,
		'dedication': DEDICATION OF THE BOOK,
		'motto': MOTTO OF THE BOOK,
		'motto_aut': AUTHOR OF THE MOTTO,
		'edition': EDITION DESCRIPTION,
		'signature': LIBRARY INFO,
	},	

	# The poem itself encoded as a list of lists (stanzas x lines)
	'body' : [ [
		{
			'text': TEXT OF THE LINE,
			'stress': BITSTRING ENCODING STRESSED (1) and UNSTRESSED (0) SYLLABLES,
			'rhyme': RHYME INDEX (the lines that rhyme all share the same value here),

			# List of meters assigned to the line
			# (in rare cases of ambiguous line, different meters may be assigned to it)
			'meter': [{
				'type': J=iamb / T=trochee / D = dactyl / A = amphibrach / X = dactylotrochee / 
					Y = dactylotrochee with anacrusis / hexameter / pentameter / N = not recognized,
				'clause': TYPE OF LINE ENDING (f=feminine, m=masculine, a=acatalectic),
				'foot': NUMBER OF FOOT,
				'pattern': PATTERN OF STRONG(S) AND WEAK(W) POSITIONS,
			}, ...],

			# List of words and their metadata
			'words': [{
			      'token': WORD AS APPEARS IN THE TEXT,
			      'token_lc': LOWERCASED token,
			      'lemma': LEMMA,
			      'morph': MORPHOLOGICAL TAG (Prague positional system),
			      'xsampa': PHONETIC TRANSCRIPTION IN XSAMPA,
			      'phoebe': SIMPLIFIED PHONETIC TRANSCRIPTION (CCV INTERNAL FORMAT),
		
			}, ...],

			# Dict holding punctuation marks
			# Punctuation marks are stored under the key which corresponds
			# to the index of a word which the puntuation precedes
			# (for line-final puctuation key == len(words)
	 		'punct': {},		
		},
		...
	], ... ]
	
}

``` 



## License
[CC-BY-SA]("https://creativecommons.org/licenses/by-sa/4.0/")

Corpus of Czech verse is being built at the [Institute of Czech Literature, Czech Academy of Sciences](http://ucl.cas.cz).  Please mention this information whenever you use the data provided here. 

Furthermore we'd like to ask you to quote following articles:

> What is CCV:

```
@article{ccv2015,
	author = {Plecháč, Petr and Kolár, Robert},
	title = {The Corpus of Czech Verse},
	doi = {10.12697/smp.2015.2.1.05},
	journal = {Studia Metrica et Poetica},
	number = {1},
	volume = {2},
	year = {2015}
	pages = {107--118},
}
```
  
> How it was built:

```
@article{ccv2016,
	author = {Plecháč, Petr},
	title = {Czech Verse Processing System KVĚTA -- Phonetic and Metrical Components},
	doi = {10.1515/glot-2016-0013},
	journal = {Glottotheory},
	number = {2},
	volume = {7},
	year = {2016}
	pages = {159--174},
}
```
 
