#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#

FROM python:alpine AS build

RUN pip install --no-cache-dir httpx starlette sse_starlette uvicorn

FROM python:alpine AS run

RUN adduser -S sampan -G root
USER sampan

COPY --from=build /usr/local/lib/python3.12/site-packages /usr/local/lib/python3.12/site-packages
COPY --chown=sampan:root python /home/sampan/python
COPY --chown=sampan:root static /home/sampan/static

EXPOSE 8080
WORKDIR /home/sampan
ENTRYPOINT ["python", "python/main.py"]