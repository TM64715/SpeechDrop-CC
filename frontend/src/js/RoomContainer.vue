<template>
    <div class="container">
        <transition name="fade">
            <a v-if="fileList.length > 1" onclick="ga('send', 'event', 'Room', 'archive')"
                :href="`/${roomId}/archive`" data-tooltip="Download all files" class="button download-all-button tooltip-left"
                download>
                <img src="/static/img/download-folder.svg" class="header-button-img"
                    alt="Download icon"/>
            </a>
        </transition>
        <div class="room-header">
            <span class="room-name" v-html="roomName" />
            <div class="room-divider"></div>
            <span class="room-code">{{ roomId }}</span>
        </div>
        <transition-group id="file-grid" name="grid-entries" class="flex two three-800 five-1200 six-1800 seven-2000" tag="div">
            <div class="card-wrapper upload-wrapper" v-bind:key="-1">
                <article class="card upload-card">
                    <div id="file-dropzone">
                        <img class="passthrough-pointer" src="/static/img/upload-icon.svg" width="80" height="80" alt="Upload icon"/>
                        <p id="upload-text" class="passthrough-pointer"></p>
                    </div>
                </article>
            </div>
            <div class="card-wrapper" v-for="fileEntry in fileList" v-bind:key="fileEntry.origPos">
                <article class="card">
                    <div v-on:click.self="deleteFile(fileEntry.origPos)" class="delete-button">&#215;</div>
                    <a v-bind:href="fileEntry.url" download>
                    <header class="file-header">
                        <h3>{{ fileEntry.name }}</h3>
                        <div class="file-date">{{ fileEntry.formattedDate }}</div>
                    </header>
                    </a>
                    <div class="card-button-container">
                        <a target="_blank" rel="noopener" v-bind:href="'https://docs.google.com/gview?url=https://files.classrooms.cloud' + fileEntry.url" class="half card-button card-button-left">Preview</a>
                        <a v-bind:href="fileEntry.url" class="half card-button" download>Download</a>
                    </div>
                </article>
            </div>
        </transition-group>
    </div>
</template>
