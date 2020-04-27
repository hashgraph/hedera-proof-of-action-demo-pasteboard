<template>
<div class="box">
    <div v-if="isUploading" class="box-main">
    </div>
    <div v-else-if="notFound" class="box-main">
        <div class="label">
            Image not found
        </div>
        <div class="spacer"></div>
        <button type="button" class="btn btn-outline btn-dismiss" @click="handleDismiss">
            Dismiss
        </button>
    </div>
    <div v-else-if="check" class="box-main">
        <div class="check-label">Transaction ID</div>
        <div class="check-value">{{ check.transactionId }}</div>
        <div class="check-label">Consensus Timestamp</div>
        <div class="check-value">{{ check.timestamp }}</div>
        <div class="check-label">Running Hash</div>
        <div class="check-value">{{ check.runningHash }}</div>
        <div class="check-label">Sequence Number</div>
        <div class="check-value">{{ check.sequenceNumber }}</div>
        <div class="spacer"></div>
        <button type="button" class="btn btn-outline btn-dismiss" @click="handleDismiss">
            Dismiss
        </button>
    </div>
    <div v-else-if="file" class="box-main">
        <div class="image-name">{{ file.name }}</div>
        <img class="image-view" :src="fileURL" />
        <div class="spacer"></div>
        <button type="button" class="btn btn-upload" @click="handleUpload">
            Upload
        </button>
        <button type="button" class="btn btn-outline btn-upload" @click="handleCheckUpload">
            Check
        </button>
    </div>
    <div v-else class="box-main">
        <div class="zone" @click="handleClickUploadZone">
            <div class="label">
                Click to upload
            </div>
            <div class="sub-label">
                an image up to 1 MB
            </div>
            <button type="button" class="btn btn-select">
                Select image to upload
            </button>
            <input
                accept="image/*"
                ref="input" class="input" type="file"
                @change="handleChangeFile"
            />
        </div>
        <div class="or-message">
            or enter a transaction ID to lookup the proof
        </div>
        <div class="form-check">
            <input class="input-id" type="text" v-model="transactionId" />
            <button type="button" class="btn btn-check" @click="handleCheck">
                Check
            </button>
        </div>
    </div>
</div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    data() {
        return {
            // transaction ID to check
            transactionId: null,

            // image file that is about to be uploaded
            file: null,

            // url to image
            fileURL: null,

            // are we uploading right now?
            isUploading: false,

            // check results
            check: null,

            // was the image Id not found?
            notFound: false,
        };
    },
    methods: {
        handleClickUploadZone() {
            this.$refs.input.click();
        },

        handleChangeFile(event) {
            this.file = event.target.files[0];
            this.fileURL = URL.createObjectURL(this.file);
        },

        handleDismiss() {
            this.isUploading = false;
            this.file = null;
            this.check = null;
            this.notFound = false;
        },

        handleCheck() {
            this.notFound = true;
        },

        handleCheckUpload() {
            // this.isUploading = true;
            this.check = {
                transactionId: "0.0.21@232325t325.2332324",
                timestamp: new Date(Date.now()),
                runningHash: "1111sdfsdf",
                sequenceNumber: 2391
            };
        },

        handleUpload() {
            // this.isUploading = true;
            this.check = {
                transactionId: "0.0.21@232325t325.2332324",
                timestamp: new Date(Date.now()),
                runningHash: "1111sdfsdf",
                sequenceNumber: 2391
            };
        }
    }
});
</script>

<style>
.box {
    background: #fff;
    box-shadow: 0 0 12px 1px rgba(0, 0, 0, 0.1);
    border-radius: 6px;
    padding: 35px;
}

.box-main {
    height: 500px;
    width: 500px;
    display: flex;
    flex-direction: column;
    position: relative;
}

.zone {
    border-radius: 6px;
    display: flex;
    height: 100%;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 2px dashed #c2c2c2;
}

.input {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    opacity: 0;
    display: none;
    height: 100%;
}

.label {
    color: #252525;
    font-weight: 500;
}

.sub-label {
    color: #252525;
    margin-top: 4px;
    opacity: 0.9;
}

.spacer {
    flex: 1;
}

.btn {
    appearance: none;
    border: none;
    color: #fff;
    outline: none;
    font-weight: 600;
    background-color: #8259ef;
    cursor: pointer;
    border-radius: 6px;
    font-size: 14px;
    padding: 14px 22px;
}

.btn-outline {
    color: #8259ef;
    background-color: transparent;
    border: 1px solid currentColor;
}

.btn-select {
    margin-top: 50px;
}

.btn-upload {
    width: 100%;
}

.btn-upload.btn-outline {
    margin-top: 15px;
}

.btn:hover {
    background-color: #6b3bec;
}

.btn-outline:hover {
    background-color: unset;
    color: #6b3bec;
}

.image-name {
    font-weight: 500;
    margin-bottom: 10px;
    opacity: 0.7;
}

.image-view {
    border-radius: 6px;
    object-fit: contain;
    border: 1px solid #e2e2e2;
    background-color: #fafafa;
    width: 100%;
    height: 300px;
}

.form-check {
    display: flex;
}

.btn-check {
}

.or-message {
    opacity: 0.5;
    margin-top: 20px;
    margin-bottom: 20px;
    text-align: center;
}

.input-id {
    width: 100%;
    margin-right: 10px;
    border: 1px solid #929292;
    border-radius: 6px;
    font-size: 16px;
    padding: 12px;
}

.input-id:focus {
    box-shadow: 0 0 0 1px #8259ef;
    outline: none;
}

.check-label {
    font-size: 14px;
    font-weight: 500;
    opacity: 0.7;
    margin-bottom: 5px;
    color: #252525;
}

.check-value {
    font-size: 16px;
    color: #252525;
    margin-bottom: 15px;
}
</style>
