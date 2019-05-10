sudo npm install -g @vue/cli @vue/cli-init

vue init nativescript-vue/vue-cli-template [프로젝트명]



? Project name jw_sh_calc_prj

? Project description It is calculator application

? Application name CalcPrj

? Unique application identifier org.nativescript.application

? Project version 1.0.0

? Author 

? License MIT

? Select the programming language javascript

? Select a preset (more coming soon) TabView

? Install vuex? (state management) No

? Install vue-devtools? No

? Color scheme light



   vue-cli · Generated "[프로젝트명]".

   vue-cli · cd [디렉토리명]

   vue-cli · npm install

   vue-cli · tns run android --bundle

   vue-cli · # or

   vue-cli · tns run ios --bundle

   vue-cli · --

   vue-cli · You may also try the new HMR mode by replacing --bundle

   vue-cli · with --hmr, but note that this is a beta feature.



VisualStudioCode에 터미널에서 다음 명령어를 실행한다

- 예뮬레이터로 실행할 경우

tns run android --emulator --bundle

- 실제 기기에서 실행할 경우

tns device

tns run android --device [디바이스 식별자] --bundle