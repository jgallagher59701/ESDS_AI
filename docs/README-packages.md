To get pdftotext, Get python 3 and then,  `brew install pkg-config poppler` and
then `pip install pdftotext`

To get latex on OSX: `brew install  --cask basictex`

Set up the path: 
echo 'export PATH="/Library/TeX/texbin:$PATH"' >> ~/.zshrc
source ~/.zshrc

Then, install TeX live manager

`sudo tlmgr update --self`
`sudo tlmgr install <package_name>`

