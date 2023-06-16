<script lang="ts" setup>
</script>

<template>
    <div style="padding-left: 20px;">Comments</div>
            <div class="comment-section">
              <div class="comment">
                <div class="comment-layout">
                  <img src="src/components/explore/components/assets/cat-pic.jpg" class="commenter-image" />
                </div>
                <div class="comment-layout">
                  This is first comment.
                </div>
              </div>
              <div class="comment">
                  This is second comment.
              </div>
              <div class="comment">
                  This is third comment.
              </div>
              <div class="comment">
                  This is fourth comment.
              </div>
              <div class="comment">
                  This is fifth comment.
              </div>
              <div class="comment">
                  This is sixth comment.
              </div>
          </div>
</template>

<style lang="scss">
/* Comment Section */
.comment-section {
    max-height: 25vh;
    max-width: 100%;
    overflow-y: scroll;
}
 
.comment {
    height: 10%;
    margin: 2%;
    padding: 20px;
    background-color: #ffff;
    color: black;
}

.comment-layout {
    width: 50%;
    padding: 20px;
    float: left;
}

.commenter-image {
    width: 10%;
    height: auto;
    border-radius: 50%;
    position: absolute;
    top: 30px;
    left: 30px;
}
</style>