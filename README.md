# PhishIntention

## PhishIntention
- This is the repository for phishintention project
    
### [Framework]
    
<img src="big_pic/pic.jpg" style="width:2000px;height:350px"/>

```Input```: a screenshot, ```Output```: Phish/Benign, Phishing target
- Step 1: Enter <b>Layout detector</b>, get predicted elements

- Step 2: Enter <b>Siamese</b>
    - If Siamese report no target, ```Return  Benign, None```
    - Else Siamese report a target, Enter step 3 <b>CRP classifier(and HTML heuristic)</b>
       
- Step 3: <b>CRP classifier(and HTML heuristic)</b>
   - If <b>CRP classifier(and heuristic)</b> reports its a CRP page, go to step 5 <b>Return</b>
   - ElIf not a CRP page and havent execute <b>Dynamic analysis</b> before, go to step 4: <b>Dynamic analysis</b>
   - Else not a CRP page but have done <b>Dynamic analysis</b> before, ```Return Benign, None``` 

- Step 4: <b>Dynamic analysis</b>
   - Find login/signup links and click, if reach a CRP page at the end, go back to step 1 <b>Layout detector</b> with updated URL and screenshot
   - Else cannot reach a CRP page, ```Return Benign, None``` 
   
- Step 5: 
    - If reach a CRP + Siamese report target: ```Return Phish, Phishing target``` 
    - Else ```Return Benign, None``` 

### [Instructions]
- For phish discovery experiment:
-- If you want to run phishintention
```
python phishintention_main.py --folder [data folder] --results [xxx.txt]
```
-- If you want to run phishpedia instead
```
python phishpedia_main.py --folder [data folder] --results [xxx.txt]
```
- For general experiment:
please run evaluation scripts
```
python -m src.pipeline_eval --data-dir [data folder] --mode [phish|benign] --write-txt [output.txt] --exp [pedia|intention] --ts [threshold for siamese]
```

### [Project structure]
- src
    - credential_classifier: training scrip for CRP classifier
    - layout_matcher: script for layout matcher and layout heuristic
    - phishpedia: training script for siamese
    - element_detector: training script for element detector
    - util: other scripts (chromedriver utilities)
    
    - element_detector.py: main script for element detector
    - credential.py: main script for CRP classifier
    - layout.py: main script for layout 
    - siamese.py: main script for siamese
    - login_finder.py: main script for dynamic login finder

        