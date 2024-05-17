docker build -t jeykll -f Dockerfile.base .
mkdir docs
docker run -w /docs -v`pwd`/docs:/docs --entrypoint jekyll jekyll new --skip-bundle .

sed -ibak 's/^gem "jekyll",/#gem "jekyll",/' docs/Gemfile
sed -ibak '/# gem "github-pages"/s/# //' docs/Gemfile
sed -ibak '/gem "github-pages"/s/,/, "~> 231" ,/' docs/Gemfile

docker build -t jkserve .
docker run -w /docs -v`pwd`/docs:/docs -p 4000:4000 jkserve
