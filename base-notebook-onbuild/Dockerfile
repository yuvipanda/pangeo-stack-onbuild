FROM pangeo/base-notebook:2019.03.12

ONBUILD COPY --chown=1000:1000 . ${REPO_DIR}

ONBUILD RUN if test -f ${REPO_DIR}/environment.yml; then \
                conda env update -n root -f ${REPO_DIR}/environment.yml && \
                conda clean -tipsy && \
                conda list -n root; \
            fi


ONBUILD RUN if test -f ${REPO_DIR}/postBuild; then \
                chmod +x ${REPO_DIR}/postBuild && \
                ${REPO_DIR}/postBuild; \
            fi