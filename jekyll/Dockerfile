FROM jekyll

USER root
WORKDIR /docs
COPY docs/ /docs/
RUN bundle install  && \
	bundle add webrick
RUN echo "host: 0.0.0.0" >> _config.yml	
ENTRYPOINT ["bundle"] 	
CMD  ["exec","jekyll","serve"]
