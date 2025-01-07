<script setup>
import { ref } from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';
import { Link } from '@inertiajs/vue3';

const showingNavigationDropdown = ref(false);
</script>

<template>
    <div class="container">
        <!-- Page Navigation -->
        <nav>
            <!-- Primary Navigation Menu -->
            <div class="menu-primary">
                <div class="navigation">
                    <!-- Logo -->
                    <div class="logo-container">
                        <Link :href="route('dashboard')">
                            <ApplicationLogo class="logo" />
                        </Link>
                    </div>

                    <!-- Navigation Links -->
                    <div
                        class="links-container"
                    >
                        <NavLink
                            :href="route('dashboard')"
                            :active="route().current('dashboard')"
                        >
                            Dashboard
                        </NavLink>
                    </div>
                </div>

                <div class="dropdown-container">
                    <!-- Settings Dropdown -->
                    <div>
                        <Dropdown align="right" width="48">
                            <template #trigger>
                                <span class="dropdown-button">
                                    <button
                                        type="button"
                                    >
                                        {{ $page.props.auth.user.name }}

                                        <svg
                                            xmlns="http://www.w3.org/2000/svg"
                                            viewBox="0 0 20 20"
                                            fill="currentColor"
                                        >
                                            <path
                                                fill-rule="evenodd"
                                                d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                                clip-rule="evenodd"
                                            />
                                        </svg>
                                    </button>
                                </span>
                            </template>

                            <template #content>
                                <DropdownLink
                                    :href="route('profile.edit')"
                                >
                                    Profile
                                </DropdownLink>
                                <DropdownLink
                                    :href="route('logout')"
                                    method="post"
                                    as="button"
                                >
                                    Log Out
                                </DropdownLink>
                            </template>
                        </Dropdown>
                    </div>
                </div>

                <!-- Hamburger -->
                <div class="hamburger">
                    <button
                        @click="
                            showingNavigationDropdown =
                                !showingNavigationDropdown
                        "
                    >
                        <svg
                            stroke="currentColor"
                            fill="none"
                            viewBox="0 0 24 24"
                        >
                            <path
                                :class="{
                                    hidden: showingNavigationDropdown,
                                    visible: !showingNavigationDropdown,
                                }"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                stroke-width="2"
                                d="M4 6h16M4 12h16M4 18h16"
                            />
                            <path
                                :class="{
                                    hidden: !showingNavigationDropdown,
                                    visible: showingNavigationDropdown,
                                }"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                stroke-width="2"
                                d="M6 18L18 6M6 6l12 12"
                            />
                        </svg>
                    </button>
                </div>
            </div>

            <!-- Responsive Navigation Menu -->
            <div
                :class="{
                    visible: showingNavigationDropdown,
                    hidden: !showingNavigationDropdown,
                }"
                class="menu-responsive"
            >
                <div class="links-container">
                    <ResponsiveNavLink
                        :href="route('dashboard')"
                        :active="route().current('dashboard')"
                    >
                        Dashboard
                    </ResponsiveNavLink>
                </div>

                <!-- Responsive Settings Options -->
                <div
                    class="settings-container"
                >
                    <div class="settings-user">
                        <div
                            class="username"
                        >
                            {{ $page.props.auth.user.name }}
                        </div>
                        <div class="email">
                            {{ $page.props.auth.user.email }}
                        </div>
                    </div>

                    <div class="settings-content">
                        <ResponsiveNavLink :href="route('profile.edit')">
                            Profile
                        </ResponsiveNavLink>
                        <ResponsiveNavLink
                            :href="route('logout')"
                            method="post"
                            as="button"
                        >
                            Log Out
                        </ResponsiveNavLink>
                    </div>
                </div>
            </div>
        </nav>

        <!-- Page Heading -->
        <header v-if="$slots.header">
            <div>
                <slot name="header" />
            </div>
        </header>

        <!-- Page Content -->
        <main>
            <slot />
        </main>
    </div>
</template>

<style lang="scss" scoped>
.container {
    min-height: 100vh;
    background-color: #f3f4f6;
}

nav {
    background-color: #ffffff;
    border-bottom: 1px solid #f3f4f6;

    .menu-primary {
        max-width: 80rem;
        height: 4rem;

        margin: 0 auto;
        padding: 0 1rem;

        display: flex;
        justify-content: space-between;

        .navigation {
            display: flex;

            .logo-container {
                display: flex;
                flex-shrink: 0;
                align-items: center;

                .logo {
                    display: block;
                    
                    width: auto;
                    height: 2.25rem;

                    color: #1f2937;
                    fill: currentColor;
                }
            }

            .links-container {
                display: none;
                margin-left: 2rem;
            }
        }

        .dropdown-container {
            display: none;

            & > div {
                position: relative;
                margin-inline-start: 0.75rem;
            }

            .dropdown-button {
                display: flex;
                border-radius: 0.375rem;

                button {
                    display: inline-flex;
                    align-items: center;

                    padding: 0.5rem 0.75rem;

                    border-radius: 0.375rem;
                    border: 1px solid transparent;

                    background-color: #ffffff;
                    color: #6b7280;

                    font-size: 0.875rem;
                    line-height: 1rem;
                    font-weight: 500;

                    transition-property: color, background-color;
                    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
                    transition-duration: 0.15s;

                    &:hover {
                        color: #374151;
                    }

                    &:focus {
                        outline: 2px solid transparent;
                        outline-offset: 2px;
                    }

                    svg {
                        width: 1rem;
                        height: 1rem;

                        margin-inline-start: 0.5rem;
                        margin-inline-end: -0.125rem;
                    }
                }
            }
        }

        .hamburger {
            margin-inline-end: -0.5rem;

            display: flex;
            align-items: center;

            button {
                display: inline-flex;
                align-items: center;
                justify-content: center;

                border-radius: 0.375rem;

                padding: 0.5rem;

                background-color: transparent;
                color: #9ca3af;
                border: none;

                transition-property: color, background-color;
                transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
                transition-duration: 0.15s;

                &:hover, &:focus {
                    background-color: #f3f4f6;
                    color: #6b7280;
                }

                &:focus {
                    outline: 2px solid transparent;
                    outline-offset: 2px;
                }

                svg {
                    width: 1.5rem;
                    height: 1.5rem;

                    path.hidden {
                        display: none;
                    }

                    path.visible {
                        display: inline-flex;
                    }
                }
            }
        }
    }

    .menu-responsive {
        &.visible {
            display: block;
        }

        &.hidden {
            display: none;
        }

        .links-container {
            margin-top: 0.25rem;
            padding-top: 0.5rem;
            padding-bottom: 0.75rem;
        }

        .settings-container {
            padding-top: 1rem;
            padding-bottom: 0.25rem;

            border-top: 1px solid #e5e7eb;

            .settings-user {
                padding: 0 1rem;

                .username {
                    font-size: 1rem;
                    line-height: 1.5rem;
                    font-weight: 500;

                    color: #1f2937;
                }

                .email {
                    font-size: 0.875rem;
                    line-height: 1.25rem;
                    font-weight: 500;

                    color: #6b7280;
                }
            }
        }
    }
}

header {
    background-color: #ffffff;
    box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px -1px rgba(0, 0, 0, 0.1);

    & > div {
        max-width: 80rem;

        margin: 0 auto;
        padding: 1.5rem 1rem;
    }
}

@media (min-width: 640px) {
    header > div {
        padding: 1.5rem;
    }

    nav .menu-primary {
        padding: 0 1.5rem;

        .navigation .links-container {
            margin-top: -1px;
            margin-bottom: -1px;
            margin-inline-start: 2.5rem;
            display: flex;
        }

        .dropdown-container {
            margin-inline-start: 1.5rem;
            display: flex;
            align-items: center;
        }

        .hamburger {
            display: none;
        }
    }

    nav .menu-responsive {
        display: none;
    }
}

@media (min-width: 1024px) {
    header > div {
        padding: 1rem 2rem;
    }

    nav .menu-primary {
        padding: 0 2rem;
    }
}
</style>
