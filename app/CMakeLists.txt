###########################################################################
# Copyright 2015, 2016, 2017 IoT.bzh
#
# author: Fulup Ar Foll <fulup@iot.bzh>
# contrib: Sebastien Douheret <sebastien.douheret@iot.bzh>
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
###########################################################################

# Add target to project dependency list
PROJECT_TARGET_ADD(helloworld-app)

	# build for prod or development
	#set(HTML_MODE prod)
	set(HTML_MODE dev)

	# Define project Targets
	add_custom_command(OUTPUT dist.${HTML_MODE}
		DEPENDS ${TARGET_NAME}
		WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
		COMMAND [ -d "dist.${HTML_MODE}" ] || npm install
		COMMAND [ -d "dist.${HTML_MODE}" ] || gulp build-app-${HTML_MODE}
		COMMAND touch dist.${HTML_MODE}
		COMMAND cp -r dist.${HTML_MODE} ${CMAKE_CURRENT_BINARY_DIR}
	)

	add_custom_target(${TARGET_NAME} ALL DEPENDS dist.${HTML_MODE})

	# Binder exposes a unique public entry point
	SET_TARGET_PROPERTIES(${TARGET_NAME} PROPERTIES
		LABELS "HTDOCS"
		OUTPUT_NAME dist.${HTML_MODE}
	)

