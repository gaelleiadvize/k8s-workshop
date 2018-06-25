# Copyright 2016, Google, Inc.
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# [START all]
# FROM node:6-alpine
# EXPOSE 8080
# COPY server.js .
# CMD node server.js
# [END all]


FROM node:9-alpine AS builder

ARG NODE_ENV
ENV NODE_ENV $NODE_ENV

WORKDIR /app

COPY package.json yarn.lock /app/

RUN yarn --pure-lockfile

FROM node:9-alpine
WORKDIR /app
COPY --from=builder /app /app
COPY . /app

RUN chown -R node:node /app/* 

USER node

EXPOSE 8080

CMD ["yarn", "start"]