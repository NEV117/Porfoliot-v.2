<template>
  <main v-if="!loading" id="about-me" class="page">
    <div id="mobile-page-title">
      <h2>_about-me</h2>
    </div>

    <div id="page-menu" class="w-full flex !min-w-[400px]">
      <!-- DESKTOP section icons -->
      <div id="sections">
        <div
          id="section-icon"
          v-for="section in config.dev.about.sections"
          :key="section.title"
          :class="{ active: isSectionActive(section.title) }"
        >
          <img
            :id="'section-icon-' + section.title"
            :src="section.icon"
            :alt="section.title + '-section'"
            @click="focusCurrentSection(section)"
          />
        </div>
      </div>

      <!-- focused section content -->
      <div
        id="section-content"
        class="hidden lg:block w-full h-full border-right"
      >
        <!-- title -->
        <div
          id="section-content-title"
          class="hidden lg:flex items-center min-w-full"
          @click="open('section-icon')"
        >
          <img
            id="section-arrow-menu"
            src="/icons/arrow.svg"
            alt="section-arrow-menu"
            class="section-arrow mx-3 open"
          />
          <p
            v-html="config.dev.about.sections[currentSection].title"
            class="font-fira_regular text-white text-sm"
          ></p>
        </div>

        <!-- folders -->
        <div id="folderContent">
          <div
            v-for="(folder, key, index) in config.dev.about.sections[
              currentSection
            ].info"
            :key="key"
            class="grid grid-cols-2 items-center my-2 font-fira_regular text-menu-text"
            @click="focusCurrentFolder(folder)"
          >
            <div class="flex col-span-2 hover:text-white hover:cursor-pointer">
              <img
                id="diple"
                src="/icons/diple.svg"
                alt=""
                :class="{ open: isOpen(folder.title) }"
              />
              <img
                :src="'/icons/folder' + (index + 1) + '.svg'"
                alt=""
                class="mr-3"
              />
              <p
                :id="folder.title"
                v-html="key"
                :class="{ active: isActive(folder.title) }"
              ></p>
            </div>
            <div v-if="folder.files !== undefined" class="col-span-2">
              <div
                v-for="(file, key) in folder.files"
                :key="key"
                class="hover:text-white hover:cursor-pointer flex my-2"
              >
                <img src="/icons/markdown.svg" alt="" class="ml-8 mr-3" />
                <p>{{ key }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- contact -->
        <div
          id="section-content-title-contact"
          class="flex items-center min-w-full border-top"
        >
          <img
            id="section-arrow-menu"
            src="/icons/arrow.svg"
            alt=""
            class="section-arrow mx-3 open"
          />
          <p
            v-html="config.dev.contacts.direct.title"
            class="font-fira_regular text-white text-sm"
          ></p>
        </div>
        <div id="contact-sources" class="hidden lg:flex lg:flex-col my-2">
          <div
            v-for="(source, key) in config.dev.contacts.direct.sources"
            :key="key"
            class="flex items-center mb-2"
          >
            <img :src="'/icons/' + key + '.svg'" alt="" class="mx-4" />
            <a
              v-html="source"
              href="/"
              class="font-fira_retina text-menu-text hover:text-white"
            ></a>
          </div>
        </div>
      </div>

      <!-- mobile -->
      <div id="section-content" class="lg:hidden w-full font-fira_regular">
        <div v-for="section in config.dev.about.sections" :key="section.title">
          <!-- section title (mobile) -->
          <div
            :key="section.title"
            :src="section.icon"
            id="section-content-title"
            class="flex lg:hidden mb-1"
            @click="focusCurrentSection(section)"
          >
            <img
              src="/icons/arrow.svg"
              :id="'section-arrow-' + section.title"
              alt=""
              class="section-arrow"
            />
            <p v-html="section.title" class="text-white text-sm"></p>
          </div>

          <!-- folders -->
          <div :id="'folders-' + section.title" class="hidden">
            <!-- <div :id="'folders-' + section.title" :class="currentSection == section.title ? 'block' : 'hidden'"> -->
            <div
              v-for="(folder, key, index) in config.dev.about.sections[
                section.title
              ].info"
              :key="key"
              class="grid grid-cols-2 items-center my-2 font-fira_regular text-menu-text hover:text-white hover:cursor-pointer"
              @click="focusCurrentFolder(folder)"
            >
              <div class="flex col-span-2">
                <img id="diple" src="/icons/diple.svg" />
                <img
                  :src="'icons/folder' + (index + 1) + '.svg'"
                  alt=""
                  class="mr-3"
                />
                <p
                  :id="folder.title"
                  v-html="key"
                  :class="{ active: isActive(folder.title) }"
                ></p>
              </div>
              <div v-if="folder.files !== undefined" class="col-span-2">
                <div
                  v-for="(file, key) in folder.files"
                  :key="key"
                  class="hover:text-white hover:cursor-pointer flex my-2"
                >
                  <img src="/icons/markdown.svg" alt="" class="ml-8 mr-3" />
                  <p>{{ key }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- section content title -->
        <div
          id="section-content-title"
          class="flex items-center min-w-full"
          @click="showContacts()"
        >
          <img
            src="/icons/arrow.svg"
            alt=""
            id="section-arrow"
            class="section-arrow"
          />
          <p
            v-html="config.dev.contacts.direct.title"
            class="font-fira_regular text-white text-sm"
          ></p>
        </div>

        <!-- section content folders -->
        <div id="contacts" class="hidden">
          <div
            v-for="(source, key) in config.dev.contacts.direct.sources"
            :key="key"
            class="flex items-center my-2"
          >
            <img :src="'/icons/' + key + '.svg'" alt="" />
            <a
              v-html="source"
              href="/"
              class="font-fira_retina text-menu-text hover:text-white ml-4"
            ></a>
          </div>
        </div>
      </div>
    </div>
    <!-- MENU END -->

    <!-- content -->
    <div class="flex flex-col lg:grid lg:grid-cols-2 h-full w-full">
      <div id="left" class="w-full flex flex-col border-right">
        <!-- windows tab desktop -->
        <div class="tab-height w-full hidden lg:flex border-bot items-center">
          <div class="flex items-center border-right h-full">
            <p
              v-html="config.dev.about.sections[currentSection].title"
              class="font-fira_regular text-menu-text text-sm px-3"
            ></p>
            <img src="/icons/close.svg" alt="" class="mx-3" />
          </div>
        </div>

        <!-- windows tab mobile -->
        <div id="tab-mobile" class="flex lg:hidden font-fira_retina">
          <span class="text-white">// </span>
          <h3
            v-html="config.dev.about.sections[currentSection].title"
            class="text-white px-2"
          ></h3>
          <span class="text-menu-text"> / </span>
          <h3
            v-html="
              config.dev.about.sections[currentSection].info[folder].title
            "
            class="text-menu-text pl-2"
          ></h3>
        </div>

        <!-- text -->
        <div
          id="commented-text"
          class="flex h-full w-full lg:border-right overflow-auto"
        >
          <div class="w-full h-full ml-5 mr-10 lg:my-5 overflow-scroll">
            <CommentedText
              :text="
                config.dev.about.sections[currentSection].info[folder]
                  .description
              "
            />
          </div>

          <!-- scroll bar -->
          <div
            id="scroll-bar"
            class="h-full border-left hidden lg:flex justify-center py-1"
          >
            <div id="scroll"></div>
          </div>
        </div>
      </div>

      <div id="right" class="max-w-full flex flex-col">
        <!-- windows tab -->
        <div
          class="tab-height w-full h-full hidden lg:flex border-bot items-center"
        ></div>

        <!-- windows tab mobile -->
        <div
          class="tab-height w-full h-full flex-none lg:hidden items-center"
        ></div>

        <div
          id="gists"
          class="flex flex-col lg:px-6 lg:py-4 w-full overflow-hidden"
        >
          <div class="flex flex-col overflow-scroll">
            <!-- snippets or custom content based on selected folder -->
            <template v-if="folder === 'experience'">
              <!-- Custom content for 'experience' folder -->
              <div data-aos="fade-down" class="rounded-md">
                <div
                  class="group relative grid pb-1 transition-all sm:grid-cols-8 sm:gap-8 md:gap-4 lg:hover:!opacity-100 lg:group-hover/list:opacity-50"
                >
                  <div
                    class="absolute bg-slate-900 -inset-x-3 -inset-y-4 z-0 hidden rounded-md transition motion-reduce:transition-none lg:-inset-x-6 lg:block lg:group-hover:bg-slate-800/50 lg:group-hover:shadow-[inset_0_1px_0_0_rgba(148,163,184,0.1)] lg:group-hover:drop-shadow-lg"
                  ></div>
                  <header
                    class="z-10 mb-2 mt-1 pl-8 pt-4 text-xs font-semibold uppercase tracking-wide text-slate-500 sm:col-span-2"
                    aria-label="May 2023 - Present"
                  >
                    May 2023 - Nov 2023
                  </header>
                  <div class="z-10 sm:col-span-6 pr-5 pt-5 pb-5">
                    <h3 class="font-medium leading-snug text-slate-200">
                      <div>
                        <a
                          class="inline-flex items-baseline font-medium leading-tight text-slate-200 hover:text-teal-300 focus-visible:text-teal-300 group/link text-base"
                          rel="noreferrer"
                          aria-label="Lead Engineer at Upstatement"
                          ><span
                            class="absolute -inset-x-4 -inset-y-2.5 hidden rounded md:-inset-x-6 md:-inset-y-4 lg:block"
                          ></span
                          ><span
                            >Lloreda Project·<!-- -->
                            <span class="inline-block"
                              >Global-BI S.A.S<svg
                                xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 20 20"
                                fill="currentColor"
                                class="inline-block h-4 w-4 shrink-0 transition-transform group-hover/link:-translate-y-1 group-hover/link:translate-x-1 group-focus-visible/link:-translate-y-1 group-focus-visible/link:translate-x-1 motion-reduce:transition-none ml-1 translate-y-px"
                                aria-hidden="true"
                              >
                                <path
                                  fill-rule="evenodd"
                                  d="M5.22 14.78a.75.75 0 001.06 0l7.22-7.22v5.69a.75.75 0 001.5 0v-7.5a.75.75 0 00-.75-.75h-7.5a.75.75 0 000 1.5h5.69l-7.22 7.22a.75.75 0 000 1.06z"
                                  clip-rule="evenodd"
                                ></path></svg></span></span
                        ></a>
                      </div>
                      <div>
                        <div class="text-slate-500" aria-hidden="true">
                          Full Stack Engineer
                        </div>
                      </div>
                    </h3>
                    <p class="mt-2 text-slate-400 text-sm leading-normal">
                      Collaborated with a team of developers to design and implement software solutions for a client. Followed Agile methodologies to ensure efficient project delivery.
                    </p>
                    <ul
                      class="mt-2 flex flex-wrap"
                      aria-label="Technologies used"
                    >
                      <li class="mr-1.5 mt-2">
                        <div
                          class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                        >
                          Angular
                        </div>
                      </li>
                      <li class="mr-1.5 mt-2">
                        <div
                          class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                        >
                          .NET Core
                        </div>
                      </li>
                      <li class="mr-1.5 mt-2">
                        <div
                          class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                        >
                          SQL Server
                        </div>
                      </li>
                      <li class="mr-1.5 mt-2">
                        <div
                          class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                        >
                          TypeScript
                        </div>
                      </li>
                      <li class="mr-1.5 mt-2">
                        <div
                          class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                        >
                          ABP BoilerPlate
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </template>
            <template v-else-if="folder === 'hard-skills'">
              <!-- Custom content for 'hard-skills' folder -->
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['2']"
              />
              <!-- Primer acordeón -->
              <div id="backendSkills" class="submenu">
                <div class="title" @click="toggleAccordion('backendAccordion')">
                  <img
                    :class="{ 'rotate-arrow': isArrowRotated.backendAccordion }"
                    class="arrow"
                    src="/icons/arrow.svg"
                  />
                  <h3>Backend</h3>
                </div>
                <div
                  id="backendLinks"
                  v-if="openAccordion === 'backendAccordion'"
                >
                  <ul
                    class="mt-2 pl-3.5 flex flex-wrap"
                    aria-label="Technologies used"
                  >
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Java Spring Boot
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        .NET Core
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        NodeJS
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Express
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Prisma
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Python FLask
                      </div>
                    </li>
                  </ul>
                </div>
              </div>

              <!-- Segundo acordeón -->
              <div id="frontendSkills" class="submenu">
                <div
                  class="title"
                  @click="toggleAccordion('frontendAccordion')"
                >
                  <img
                    :class="{
                      'rotate-arrow': isArrowRotated.frontendAccordion,
                    }"
                    class="arrow"
                    src="/icons/arrow.svg"
                  />
                  <h3>FrontEnd</h3>
                </div>
                <div
                  id="frontendLinks"
                  v-if="openAccordion === 'frontendAccordion'"
                >
                  <ul
                    class="mt-2 pl-3.5 flex flex-wrap"
                    aria-label="Technologies used"
                  >
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        ReactJS
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        NextJS
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Angular
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Vue
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        HTML
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        CSS
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        TailwindCss
                      </div>
                    </li>
                  </ul>
                </div>
              </div>

              <!-- tercer acordeón -->
              <div id="otherSkills" class="submenu">
                <div class="title" @click="toggleAccordion('otherAccordion')">
                  <img
                    :class="{ 'rotate-arrow': isArrowRotated.otherAccordion }"
                    class="arrow"
                    src="/icons/arrow.svg"
                  />
                  <h3>Others</h3>
                </div>
                <div id="otherLinks" v-if="openAccordion === 'otherAccordion'">
                  <ul
                    class="mt-2 pl-3.5 flex flex-wrap"
                    aria-label="Technologies used"
                  >
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Git
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Java
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        C#
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        TypeScript
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        JavaScript
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        Python
                      </div>
                    </li>
                    <li class="mr-1.5 mt-2">
                      <div
                        class="flex items-center rounded-full bg-teal-400/10 px-3 py-1 text-xs font-medium leading-5 text-teal-300"
                      >
                        TensorFlow
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </template>
            <template v-else-if="folder === 'soft-skills'">
              <!-- Custom content for 'soft-skills' folder -->
              <div class="BubblesContainer">
                <div class="bubble">
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                </div>
                <div class="bubble">
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                </div>
                <div class="bubble">
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                </div>
                <div class="bubble">
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                </div>
                <div class="bubble">
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                  <span></span>
                </div>
              </div>
            </template>
            <template v-else-if="folder === 'interests'">
              <!-- title -->
              <h3 class="text-white lg:text-menu-text mb-4 text-sm">
                // Code snippet showcase:
              </h3>
              <!-- Default content if none of the above conditions match -->
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['7']"
              />
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['4']"
              />            
            </template>
            <template v-else-if="folder === 'education'">
              <!-- title -->
              <h3 class="text-white lg:text-menu-text mb-4 text-sm">
                // Code snippet showcase:
              </h3>
              <!-- Default content if none of the above conditions match -->
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['6']"
              />
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['5']"
              />            
            </template>
            <template v-else-if="folder === 'sports'">
              <!-- title -->
              <h3 class="text-white lg:text-menu-text mb-4 text-sm">
                // Code snippet showcase:
              </h3>
              <!-- Default content if none of the above conditions match -->
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['8']"
              />
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['9']"
              />            
            </template>
            <template v-else>
              <!-- title -->
              <h3 class="text-white lg:text-menu-text mb-4 text-sm">
                // Code snippet showcase:
              </h3>
              <!-- Default content if none of the above conditions match -->
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['1']"
              />
              <GistSnippet
                data-aos="fade-down"
                :id="config.public.dev.gists['2']"
              />
              <!-- <GistSnippet data-aos="fade-down" v-for="(gist, key) in config.public.dev.gists" :key="key" :id="gist" /> -->
            </template>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
#sections {
  width: 5rem;
  /* 80px */
  height: 100%;
  display: none;
  border-right: 1px solid #1e2d3d;
}

/* LG */
@media (min-width: 1024px) {
  #sections {
    display: block;
  }
}

#section-icon {
  @apply my-6 hover:cursor-pointer flex justify-center;
  opacity: 0.4;
}

#section-icon.active {
  opacity: 1;
}

#section-icon:hover {
  opacity: 1;
}

.tab-height {
  min-height: 35px;
  max-height: 35px;
}

#tab-mobile {
  padding: 25px 20px 0px 25px;
  align-items: flex-end;
}

#scroll-bar {
  width: 20px;
}

#scroll {
  width: 14px;
  height: 7px;
  background-color: #607b96;
}

#diple {
  @apply mx-3 w-2 max-w-fit;
}

.open {
  transform: rotate(90deg);
}

.active {
  color: white;
}

#right,
#left {
  height: 100%;
  overflow: hidden;
}

#gists-content {
  height: 100%;
  overflow: hidden;
}

@media (max-width: 1024px) {
  #gists-content {
    height: 100%;
    padding: 0px 25px;
    overflow: hidden;
  }

  .hardskills-layout {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    padding: 1rem;
  }

  #about {
    min-height: stretch;
  }
}

.section-arrow {
  transition: 0.1s;
}

#section-content #contacts {
  padding: 0px 25px;
}

.hardskills-layout {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
  padding-top: 1rem;
}

.BubblesContainer{
  height: 600px;
  padding-top: 5rem;
  padding-left: 5rem;
  display: flex;
  align-items: center;
}

.rotate-arrow {
  transform: rotate(90deg); /* Rota la flecha 180 grados */
  transition: transform 0.3s; /* Agrega una transición suave */
}

.bubble {
  position: absolute;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  box-shadow: inset 0 0 25px rgba (255, 255, 255, 0.25);
  animation: animate_4010 8s ease-in-out infinite;
}

.bubble:nth-child(2) {
  position: relative;
  zoom: 0.45;
  left: -10px;
  top: -100px;
  animation-delay: -4s;
}

.bubble:nth-child(3) {
  position: relative;
  zoom: 0.45;
  right: -80px;
  top: -300px;
  animation-delay: -6s;
}

.bubble:nth-child(4) {
  position: relative;
  zoom: 0.35;
  left: -120px;
  bottom: -200px;
  animation-delay: -3s;
}

.bubble:nth-child(5) {
  position: relative;
  zoom: 0.5;
  left: 0px;
  top: 200px;
  animation-delay: -5s;
}

@keyframes animate_4010 {
  0%,100% {
    transform: translateY(-20px);
  }

  50% {
    transform: translateY(20px);
  }
}

.bubble::before {
  content: '';
  position: absolute;
  top: 50px;
  left: 45px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: #fff;
  z-index: 10;
  filter: blur(2px);
}

.bubble::after {
  content: '';
  position: absolute;
  top: 80px;
  left: 80px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
  z-index: 10;
  filter: blur(2px);
}

.bubble span {
  position: absolute;
  border-radius: 50%;
}

.bubble span:nth-child(1) {
  inset: 10px;
  border-left: 15px solid #0fb4ff;
  filter: blur(8px);
}

.bubble span:nth-child(2) {
  inset: 10px;
  border-right: 15px solid #ff4484;
  filter: blur(8px);
}

.bubble span:nth-child(3) {
  inset: 10px;
  border-top: 15px solid #ffeb3b;
  filter: blur(8px);
}

.bubble span:nth-child(4) {
  inset: 30px;
  border-left: 15px solid #ff4484;
  filter: blur(12px);
}

.bubble span:nth-child(5) {
  inset: 10px;
  border-bottom: 10px solid #fff;
  filter: blur(8px);
  transform: rotate(330deg);
}
</style>

<script>
export default {
  data() {
    return {
      currentSection: "personal-info",
      folder: "bio",
      loading: true,
      openAccordion: "backendAccordion", // Inicializa el primer acordeón como abierto.
      isArrowRotated: {
        backendAccordion: true, // Inicializa la flecha del primer acordeón como rotada.
        frontendAccordion: false, // Inicializa la flecha del segundo acordeón como no rotada.
        otherAccordion: false,
      },
    };
  },
  /**
   * In setup we can define the data we want to use in the component before the component is created.
   */
  setup() {
    const config = useRuntimeConfig();
    return {
      config,
    };
  },
  computed: {
    // Set active class to current page link
    isActive() {
      return (folder) => this.folder === folder;
    },
    isSectionActive() {
      return (section) => this.currentSection === section;
    },
    isOpen() {
      return (folder) => this.folder === folder;
    },
  },
  methods: {
    focusCurrentSection(section) {
      this.currentSection = section.title;
      this.folder = Object.keys(section.info)[0];

      document
        .getElementById("folders-" + section.title)
        .classList.toggle("hidden"); // show folders
      document
        .getElementById("section-arrow-" + section.title)
        .classList.toggle("rotate-90"); // rotate arrow
    },
    focusCurrentFolder(folder) {
      this.folder = folder.title;
      // handle if folder belongs to the current section. It happens when you click on a folder from a different section in mobile view.
      this.currentSection = this.config.dev.about.sections[this.currentSection]
        .info[folder.title]
        ? this.currentSection
        : Object.keys(this.config.dev.about.sections).find(
            (section) =>
              this.config.dev.about.sections[section].info[folder.title]
          );
    },
    /**
     * TODO: Hay que crear un método para que cuando se haga click en un folder, se muestren los archivos que contiene. Y si se hace click en un archivo, se muestre el contenido del archivo.
     * TODO:  Además de girar el icono del diple.
     */
    toggleFiles() {
      document.getElementById("file-" + this.folder).classList.toggle("hidden");
    },
    /* Mobile */
    showContacts() {
      document.getElementById("contacts").classList.toggle("hidden");
      document.getElementById("section-arrow").classList.toggle("rotate-90"); // rotate arrow
    },
    toggleAccordion(elementId) {
      if (this.openAccordion === elementId) {
        this.openAccordion = null;
        this.isArrowRotated[elementId] = false;
      } else {
        this.openAccordion = elementId;
        this.isArrowRotated[elementId] = true;
      }
    },
  },
  mounted() {
    this.loading = false;
  },
};
</script>
