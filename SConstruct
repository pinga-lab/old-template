import os
from templates import Manuscript

env = Environment()
env.SetDefault(TEXMFHOME=os.path.join(os.environ['HOME'], 'texmf'))
# To include the class and bibtex files in the 'classes' dir
env.Replace(TEXINPUTS='classes//:')
env.Replace(BSTINPUTS='classes//:')

builder = Manuscript(
    title='PINGA paper template',
    author=['Leonardo Uieda',
            'Vanderlei C. Oliveira Jr',
            r'Val\'eria C. F. Barbosa'],
    affil=['Universidade do Estado do Rio de Janeiro, Rio de Janeiro, Brazil.',
           r'Observat\'orio Nacional, Rio de Janeiro, Brazil.'],
    author_affil=[[0, 1], [1], [1]],
    journal='geophysics',
    heads=['Uieda et al.', 'PINGA template header'],
    bibfile='references.bib')
# Make the manuscript for submission
ms = env.Command('manuscript.tex', 'msbody.tex', builder.build_ms)
mspdf = env.PDF(target='manuscript.pdf', source=ms)
# Declare that the PDf depends on the figures so it gets rebuild when they
# change.
Depends(mspdf, Glob('figs/*.eps'))

# Make a pretty version of the paper (if the document class has this feature)
paper = env.Command('paper.tex', 'msbody.tex', builder.build_paper)
paperpdf = env.PDF(target='paper.pdf', source=paper)
Depends(paperpdf, Glob('figs/*.eps'))

# These files get generated by pdflatex
Clean(os.path.curdir, Glob('*-eps-converted-to.pdf'))

# The .pyc files are generated by Python when importing templates.py
Clean(os.path.curdir, Glob('*.pyc'))