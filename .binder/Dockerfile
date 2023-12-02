FROM rocker/binder:4.3.2
LABEL maintainer='Kris Sankaran'
COPY --chown=${NB_USER} . ${HOME}
USER ${NB_USER}



RUN wget https://github.com/krisrs1128/binder-20231206/raw/master/DESCRIPTION && R -e "options(repos = list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/2023-12-02/')); devtools::install_deps()"

RUN rm DESCRIPTION.1; exit 0
